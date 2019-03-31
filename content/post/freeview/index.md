+++
title = "Freeview from FreeSurfer"
subtitle = ""

# Add a summary to display on homepage (optional).
summary = ""

date = 2019-03-31T11:17:49+02:00
draft = false

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = []

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
  caption = ""

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""
+++

FreeSurfer is an open source software package for the analysis and visualization of structural and functional neuroimaging data. It is developed by the Laboratory for Computational Neuroimaging at the Athinoula A. Martinos Center for Biomedical Imaging.
It's a really useful tool that allow for automated processes with a hint of manual intervention,
mainly through it's GUI, Freeview.

I started using FreeSurfer and Freeview  last year and, albeit the documentation being quite
thorough, I had a harder time navigating the website than I expected.

So here are a few tricks to make your handling FreeSurfer's GUI, Freeview, easier
 and faster!


## 1. Starting Freeview
 You can start freeview by just typing `freeview` in your command line and then
 opening the files you want. Of course, you will be far better off if you write
 a small script with your usual calls.

  The command options available for Freeview are:

| Argument       | Action        |
| --------------- |:-------------- |
| -v            | load a volume file |
| -l            | load a a label file |
| -dti          | load one or more dti volumes |
| -f            | load a surface |
| -w            | load waypoints |


 I have the following script saved under my `subjects/` folder:
 ```
 export SUBJECT='<subject name>'
 freeview -v \
     $SUBJECT/mri/T1.mgz \
     $SUBJECT/mri/wm.mgz \
     $SUBJECT/mri/brainmask.mgz \
     -f \
     $SUBJECT/surf/lh.white:edgecolor=blue \
     $SUBJECT/surf/lh.pial:edgecolor=yellow \
     $SUBJECT/surf/rh.white:edgecolor=blue \
     $SUBJECT/surf/rh.pial:edgecolor=yellow
 ```

 So, if I want to analyze, let's say, subject bert's images, I just open my `freeview.sh`
 script with a text editor and change `<subject name>` to `bert` (which is this
 subject's folder name).
 Then, I can open a terminal, navigate to my `subjects/` folder and type:

 ```
 ./freeview.sh
 ```
All right, we have opened Freeview and we're ready to start interacting with the GUI!

## 2. Check out the available Freeview keyboard shortcuts!
This single trick will save you an amazing amount of time. I have been working with
CentOs and a few shortcuts I have
found by experimenting are:

| Command        | Action        |
| -------------  |:------------- |
| Alt + N        | <img src="navigate.png" style="float: left; margin-right: 10px;"/> Navigate Tool |
| Ctrl + E       | <img src="recon_edit.png" style="float: left; margin-right: 10px;"/> Recon Edit Tool|
| Ctrl + F       | Toggle all surfaces |
| Alt + C        | Alternate between volumes |
| Ctrl + P       | Toggle left side menu |
| Ctrl + T       | Point set edit |

You'll find other shortcuts under [this link](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeviewGuide/FreeviewReference/FreeviewKeyboardShortcuts). I'll copy the most useful ones here for convenience:

| Command       | Action        |
| ------------- |:------------- |
| Ctrl + S       | Save          |
| Ctrl + Z       | Undo          |
| Ctrl + Q       | Exit Freeview |
| Ctrl + O       | Load Volume |
| Up/Down Arrow Keys or PageUp/PageDown| Change slice  |
| Scroll or Drag-Right-Click | Zoom In/Zoom Out |
| Ctrl + Up/Down/Left/Right (arrow keys) | Moving volume (Panning) |
| Alt + V        | Toggle currently highlighted volume |
| Shift-Drag Left Click | Adjust Contrast/Brightness  |
| Zoom in at current location | Ctrl-Left-Click (or scroll) |
| Zoom out at current location | Ctrl-Right-Click (or scroll) |

When you're in Voxel/Recon/ROI edit mode:

| Command       | Action        |
| ------------- |:------------- |
| Draw / Fill         | Left Click |
| Erase / Erase Fill | Shift+Left Click |

That conludes this short tutorial about Freeview!
If you want to read/know more, the full Freeview Guide can be found [here](https://surfer.nmr.mgh.harvard.edu/fswiki/FreeviewGuide).





  <!-- https://discourse.gohugo.io/t/linking-to-static-files-with-hugo/8282 -->
