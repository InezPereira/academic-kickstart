+++
title = "A beginner's guide to ETH's Euler"
subtitle = ""

# Add a summary to display on homepage (optional).
summary = ""

date = 2019-07-03T15:21:13+02:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Inês Pereira"]

# Is this a featured post? (true/false)
featured = true

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = []
categories = []

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["deep-learning"]` references
#   `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
# projects = ["internal-project"]

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
[image]
  # Caption (optional)
  caption = "Portrait of Leonhard Euler by Jakob Emanuel Handmann (1753)"

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""
+++

🖍 *Nota bene*: You will need to be an ETH member to use Euler. However, this
post might still be useful if you happen to be working on another cluster which
uses the [LSF](https://en.wikipedia.org/wiki/Platform_LSF)  batch system. Also relevant: I am currently mainly using MATLAB to run my simulations, so you'll find some MATLAB specific advice.
For Python specifics, check out [this page](https://scicomp.ethz.ch/wiki/Python).
<!-- Also note that [GPUs are only provided in the Leohnard cluster](https://scicomp.ethz.ch/wiki/Getting_started_with_GPUs)
and access is restricted to shareholders. -->

⌛️ **TL;DR**: check out the end of the blog post for a practical suggestion on how
to structure your job submission scripts.

## Euler ?

[Euler](https://scicomp.ethz.ch/w/images/a/ad/Getting_started_with_Euler_(September_2016).pdf)
is the high performance computing cluster at ETH Zurich.
<!-- Its name stands for *Erweiterbarer, Umweltfreundlicher, Leistungsfähiger ETH Rechner*. -->
Like its predecessors, Euler follows a shareholder model, and is for the most part financed by its users.
These "shareholders" then receive a share of the cluster's resources (*i.e* CPU time), which is proportional to their investment.
However, a small share of Euler is financed by the IT Services and is open to all ETH members.


<p style="text-align: center;">
And that's a huge hooray for students!
</p>

Euler is really a *great* resource, but can be associated with a steep learning curve,
especially if you are not used to working with a terminal and all that jazz.

In this post, we'll go through:

- How to run your first job
- Some advanced tricks
- A template for future jobs


## Running a simple job

### Connecting to Euler
The first thing you need to do is to connect to Euler.
To do that, you either need to be within the ETH network or connected via VPN.
The only requirement to login is a valid NETHZ account (no forms to fill out 🎉).
Open a terminal and type:

```bash
ssh username@euler.ethz.ch
```
Now type in your NETHZ password... and you're in!
If this is the first time you're logging in, the only extra step is to accept the
cluster's usage rights.

### File transfer

To run your jobs, you'll need to transfer your scripts and data to the cluster.
To do so, you can use the `scp` command. The general use is as follows:
```bash
scp [options] source destination
```
<!-- There are some difference between the two commands, but I'll let you read more
about [here](https://stackoverflow.com/questions/20244585/how-does-scp-differ-from-rsync)
and [here](https://superuser.com/questions/393608/difference-between-scp-and-rsync). -->

<!-- For now, let's focus on the `scp` command.  -->
Specifically, what you'll need to type is:
```bash
scp file username@euler.ethz.ch:path/to/destination # from local computer to Euler
scp username@euler.ethz.ch:path/to/source/file path/to/destination # from Euler to local computer
```

To transfer directories, the option `-r` needs to be used:
```bash
scp -r directory username@euler.ethz.ch:path/to/destination # from local computer to Euler
scp -r username@euler.ethz.ch:path/to/source/directory path/to/destination # from Euler to local computer
```

You'll find that acquainting yourself with bash scripting will come in handy for
this type of commands. Check out the cheat sheet I left in the end of the blog post
for just that!

### A word on data storage
When it comes to personal storage, every user has access to two options:
```bash
HOME=/cluster/home/username
SCRATCH=/cluster/scratch/username
```
Home is a safe long-term storage for important data. Only *you* can access it and
the content is saved every hour (snapshot) and every night (tape backup).
You are allowed 16 GB of data or a maximum of 100 000 files.
**This is the directory (folder) you'll automatically find yourself in once you login.**

Scratch, on the other hand, is designed as a fast short-term storage. There is
*no* backup and ETH will warn you that it is *purged on a regular basis*. Your disk
quota in scratch rises to 2.5 TB and a maximum of 1 000 000 files.

To check how far away (or how close...) you are from your quota, use the command
`lquota`:

```bash
lquota
+-----------------------------+-------------+------------------+------------------+------------------+
| Storage location:           | Quota type: | Used:            | Soft quota:      | Hard quota:      |
+-----------------------------+-------------+------------------+------------------+------------------+
| /cluster/home/user          | space       |          8.85 GB |         17.18 GB |         21.47 GB |
| /cluster/home/user          | files       |            25610 |            80000 |           100000 |
+-----------------------------+-------------+------------------+------------------+------------------+
| /cluster/shadow             | space       |          4.10 kB |          2.15 GB |          2.15 GB |
| /cluster/shadow             | files       |                2 |            50000 |            50000 |
+-----------------------------+-------------+------------------+------------------+------------------+
| /cluster/scratch/user       | space       |        237.57 kB |          2.50 TB |          2.70 TB |
| /cluster/scratch/user       | files       |               29 |          1000000 |          1500000 |
+-----------------------------+-------------+------------------+------------------+------------------+
```

For more information on data storage (*e.g.* options for shareholders), be sure
to check out this [presentation](https://scicomp.ethz.ch/w/images/a/ad/Getting_started_with_Euler_(September_2016).pdf)
or this [page](https://scicomp.ethz.ch/wiki/Storage_systems).

### Using Euler
All right! Now we're ready to start using the cluster!
And it all boils down to this:
```
bsub [LSF options] job
```

Of course, the tricky part is to figure out how to use the options and what
constitutes a job.
Well, here are a few options I find particularly useful (for more, check out
  [this reference](https://scicomp.ethz.ch/wiki/LSF_mini_reference)):

| Option       | Description        |
| --------------- |:-------------- |
| `-W HH:MM`     | Allowed duration for job. Default: 04:00 hours.|
| `-R "rusage[mem=X]"` | Memory (in MB per core) required. Default: X = 1024 MB.|
| `-J jobname`   | Assigns name to job. Not necessarily unique! |
| `-w "depcond"` | Sets dependencies between jobs. More on this below.|
| `-r`         | If your node crashes, LSF will re-run the job on another node.|

Now mind you that a job can be:

- a Linux command: `bsub [LSF options] command`
- a shell script: `bsub [LSF options] < script`
- a program: `bsub [LSF options] path/to/program`

<!-- So, as you can see, different types of jobs may imply a slightly different syntax. -->

Ok, so far so good. Now, to use MATLAB, you'll first need to load it.

```bash
module load new matlab/R2018a
```

Notice that I am loading a specific version of MATLAB. For more information on how to
configure the MATLAB version you want to run, check out [this link](https://scicomp.ethz.ch/wiki/MATLAB).

Once that's done, let's say you would like to fit a model using a script you wrote beforehand.
To submit your job, you then type:
```bash
bsub -J "fitModel" matlab -singleCompThread -nodisplay -r "fit_model"
```
Pardon? What are all *those* options? It's fairly easy:

- `-singleCompThread`: forces MATLAB to use only one thread for its computations
(prevents MATLAB from overloading the compute nodes).
- `-nodisplay`: just explicitly tell MATLAB no graphical display is available.


⚠️ **#ProTip**: no `.m` at the end of your script name (bsub doesn’t require that you pass the file extension).
That has once cost me an embarrassing amount of time.

You have submitted your job and get back:
```bash
Generic job.
Job <94709747> is submitted to queue <normal.4h>.
```

That looks good. To manage your jobs, you'll then need two new commands:
`bjobs` and `bkill`, which let you monitor or kill all jobs or specific jobs
(for more details, read [this reference](https://scicomp.ethz.ch/wiki/LSF_mini_reference)).

```bash
bjobs
> JOBID      USER   STAT  QUEUE      FROM_HOST   EXEC_HOST   JOB_NAME   SUBMIT_TIME
> 94709747   jdoe   RUN   normal.4h   euler01  eu-c7-106-0  fitModel   Jul  3 07:19

bkill 0 # terminate all jobs
> Job <94709747> is being terminated
```

An alternative to `bjobs` is [bbjobs](https://scicomp.ethz.ch/wiki/Using_the_batch_system#bbjobs)
(aka better bjobs).

## More advanced tricks

Let's take things up a notch. Let's say that you need to run jobs which somehow
depend on each other. The example I'll use here is a greedy feature selection
algorithm. Don't mind the details, the important thing is you need to do your
computations in three stages:

1. Run a setup function (e.g. restructure some folders)
2. Train your models
3. Choose the best model

Now that means that you only want step 2 to kick in once the setup is ready.
That's called [job chaining](https://scicomp.ethz.ch/wiki/Job_chaining) and can
be done as follows:

```bash
bsub -J job1 command1
bsub -J job2 -w "done(job1)" command2
bsub -J job3 -w "done(job2)" command3
```

Note however that the condition for `job2` is only fulfilled if `job1` is
completed successfully. If, for some reason, `job1` crashes or is killed because
it reached the runtime or memory limit, then the dependency for `job2` is never
true and `job2` will stand, pending, forever...
If you actually, for some heartless reason, don't really care what happens to
`job1`, then you should write:

```bash
bsub -J job1 command1
bsub -J job2 -w "ended(job1)" command2
```

If step 2 involves a suite of models and you want to only start step 3
once *all* models in step 2 are finished, then you might run into a problem.

If you only have two models and don't mind writing out all the dependencies, you
can opt for:

```bash
bsub -J job1 command1 # train model 1
bsub -J job2 command2 # train model 2
bsub -J job3 -w "done(job1) && done(job2)" command3 # choose best model
```

If, on the other hand, you are fitting a lot of models in step 2, you should
consider using [job arrays](https://scicomp.ethz.ch/wiki/Job_arrays).

```bash
bsub -J job[1-10] command
```

`-J job[1-10]` defines the name of the array and the number of jobs it
will contain (in this case: 10).
You then need to get the JOBID of this job array. This is
because the JOBID will be the same for the whole job array, but different subjobs
will have different names.
To get the JOBID, one way is to use `bjobs` and just copy the JOBID (let's say: 94709747).
Then, you can write:

```bash
bsub -w "numdone(94709747,*)" -J job2 command2
```

However, if you prefer (I would) to have the JOBID extracted automatically, then
this is what you want:

```bash
JOBID=$(bsub command1 | awk '/is submitted/{print substr($2, 2, length($2)-2);}')
if [ -n "$JOBID" ]; then
        bsub -w "numdone($JOBID,*)" command2
fi
```
The first line of code will run the job it contains *and* extract the job's ID.
Filling two needs with one deed 💪.
Oh wait, but what if I need to pass the array index as an argument to a function?
That can also be done! You can pass `$LSB_JOBINDEX` as a command-line argument.
Note the backslash `\` before `$LSB_JOBINDEX`:

```bash
bsub -J "job[1-10]" matlab -nodisplay -singleCompThread -r "my_function(\$LSB_JOBINDEX)"
```

💣 Ok, now an even harder thing to do would be to set a dependency on multiple
job arrays. That can also be done, with a few bash tricks:

```bash
dep_cond="" # create a variable to store the full dependency
for i in {1..50}; do
  JOBID=$(bsub -J "job$i[1-10]" matlab -nodisplay -singleCompThread -r "my_function(\$LSB_JOBINDEX)" | awk '/is submitted/{print substr($2, 2, length($2)-2);}')
  dep_cond+=" && numdone($JOBID,*)" # add new dependencies
done

dep_cond=${dep_cond:4} # remove leading " && "

bsub -w "$dep_cond" matlab -singleCompThread -nodisplay -r "my_function2()"

```

A huge thank you to the Euler cluster support for this one! In particular to
[Oliver Byrde](https://ethz.ch/services/en/organisation/departments/it-services/people/person-detail.html?persid=88087)!

## A modest template
Here is a template of the type of scripts I like. Notice the following:

- Use of `$1`: Taking in arguments from the command line is, in my opinion, really nice.
It saves you the time of opening [vim](https://en.wikipedia.org/wiki/Vim_(text_editor))
and having to edit, save, quit. You just type your arguments and click enter!
- Use of `echo` with if/else statements to check if everything is running as planned.
- Requirement of user confirmation. Some might find this annoying, but I have
often realized, when submitting the job, that something was wrong.
Requiring me to type in a confirmatory "yes" adds an extra check.

This script reconstructs the steps we had seen before, but with multiple iterations
added, hence the for loop.

```bash
#!/bin/bash

# Loading matlab module
echo loading matlab module...
module load new matlab/R2017b

# Necessary input
arg1=$1 # takes in first input argument from command line
arg2=$2 # second input argument from command line
niter=50

# Checking important arguments
if [ "$arg2" == "'this'" ] || [ "$arg2" == "'that'" ]; then
  echo "Argument 2 recognized!"
else
  echo "Argument 2 NOT recognized! You will get an error!"
fi

# Run your loop
read -p "Run your cool script? [y: yes; n: no]" -n 1 -r
echo
if [[ $REPLY =~ ^[Yy]$ ]]; then
    for ((i = 1; i <= $niter; i++)); do
        # Run setup
        if [[ $i -eq 1 ]]; then
          bsub -J "Setup$i" matlab -singleCompThread -nodisplay -r "setup($arg1,$arg2,$i)"
        else
          last_iter=$((i-1))
          bsub -J "Setup$i" -w "done(saveBest$last_iter)" matlab -singleCompThread -nodisplay -r "setup($arg1,$arg2,$i)"
        fi
        # Fit your models
         bsub -J "fitModels$i" -w "done(Setup$i)" matlab -singleCompThread -nodisplay -r "fit_models($arg1,$arg2,$i)"
        # Save your best model
        bsub -J "saveBest$i" -w "done(fitModels$i)" matlab -singleCompThread -nodisplay -r "save_best_model($arg1,$arg2,$i)"
    done
fi

```

Compare that to a version which uses job arrays:

```bash
#!/bin/bash

# Loading matlab module
echo loading matlab module...
module load new matlab/R2017b

# Necessary input
arg1=$1 # takes in first input argument from command line
arg2=$2 # second input argument from command line
niter=50

# Run your loop
read -p "Run your cool script? [y: yes; n: no]" -n 1 -r
echo
if [[ $REPLY =~ ^[Yy]$ ]]; then
    for ((i = 1; i <= $niter; i++)); do
        # Run setup
        if [[ $i -eq 1 ]]; then
          bsub -J "Setup$i" matlab -singleCompThread -nodisplay -r "setup($arg1,$arg2,$i)"
        else
          last_iter=$((i-1))
          bsub -J "Setup$i" -w "done(saveBest$last_iter)" matlab -singleCompThread -nodisplay -r "setup($arg1,$arg2,$i)"
        fi
        # Fit your models and extract JOBID from job array
        max_sim=$((nparam-i+1))
        JOBID=$(bsub -J "fitModels$i[1-$max_sim]" -w "done(Setup$i)" matlab -singleCompThread -nodisplay -r "fit_models($arg1,$arg2,\$LSB_JOBINDEX)" | awk '/is submitted/{print substr($2, 2, length($2)-2);}')
        # Save the best model using JOBID as a dependency
        if [ -n "$JOBID" ]; then
          bsub -J "saveBest$i" -w "numdone($JOBID,*)" matlab -singleCompThread -nodisplay -r "save_best_model($arg1,$arg2,$i)"
        fi
    done
fi

```



## Other useful resources

To use Euler, you'll find yourself googling *a lot* of bash commands. In addition,
figuring out how vim works can also be overwhelming in the beginning.
To ease the pain, here are a few nice cheat sheets:

- [Bash scripting  cheat sheet](https://devhints.io/bash)
- [Vim cheat sheet](https://devhints.io/vim)


<p style="text-align: center;">
Happy computations ! 👾👾👾
</p>
