+++
title = "Post Void Residual and How to Measure It"
subtitle = ""

# Add a summary to display on homepage (optional).
summary = ""

date = 2019-04-03T20:52:23+02:00
draft = true

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

Post-void residual refers to the amount of urine present in the bladder after micturition. Why should it be important to know how much urine you're accumulating in your bladder? Because stagnant urine can be a predisposing factor for infection (theory backed up by intuition, although research yields conflicting results) and can also cause kidney lesion. Imagine a hose, blocked or semi-blocked on one side and, on the other, bound to a tap with a continuous flow of water. The tap is your kidneys. Since they won't (unless they are severely damaged) stop producing urine, a blocked bladder outflow will dilate the anatomical structures leading to the urethra, ultimately causing kidney damage as well.

Because doctors and nurses are well aware of those risks, patients are often catheterised (that means a tube is placed in the urethra to help the bladder void completely)  in situations where some degree of bladder dysfunction is expected or normal voiding made difficult, such as after surgery.

But then comes the question: when is the best time to remove the catheter? How do I know if this particular patient will accumulate too much urine or not?

Well, one of the ways one can estimate the post-void residual (PVR), is, strangely, by briefly catheterizing the patient again, directly or not long after urination. One can thus appreciate how much residual urine comes out and, if too much is drained, then the catheter is left in place. However, this method is still invasive and implies discomfort. Hence, non-invasive methods have been sought out. And, indeed, ultrasound has been used as a non-invasive method for assessing bladder volume since Holmes first described it in 1967. The problem with ultrasound is that it only gives you 2D images, so you have to come up with a geometrical model for the bladder (and, thus, a mathematical formula) in order to be able to make calculations indirectly. And this is where it gets tricky. Some assume the bladder to be a rectangular prism, others prefer to assimilate it to an ellipsoid shape and some try not to start with any given geometrical premise at all. I've read that 21 formulas have been described and, up to this date, I've set my eyes on (sadly just) 11 of them. But, because the post-micturition bladder does not conform to any geometrical shape perfectly, all of these formulae are subject to large degrees of error. And this is where correction factors come into play.

The formulae by Hakenberg <em>et al.</em> (1983), Poston <em>et al.</em> (1983) and Hartnell <em>et al.</em> (1987)) assume the shape of the post-micturition bladder to be a rectangular-based prism.

<em>(<b>Math-reminder</b>: The volume of a rectangular-based prism is Height x Width x Depth x 0.5.)</em>

By starting off with this formula, what these authors did was to measure the PVR through ultrasound and then, in the same patient and right after this first measurement, a urinary catheter was placed in order to get the true value of the PVR. Bear with me, we're almost done. So, what these authors did was to compare both methods to see how far off ultrasound was. Based on these results, the authors altered the final coefficient to 0.625, 0.7 and 0.65, respectively.

Now, the final question is, which of these coefficients should one use? I couldn't find any European guidelines on the matter and, since I'm working in Germany, I tried to see if I could find any German literature. And, indeed, the only guideline I found was one related to <em>Sonographie im Rahmen der urogynäkologischen Diagnostik</em> by the <em>Deutsche Gesellschaft für Gynäkologie und Geburtshilfe </em>(the German Society of  Obstetrics and Gynecology) where the mentioned formula was Height x Width x Depth x 0.7. Oh, and the <em>Oxford Handbook of Urology </em>also mentions it as a frequently used formula.

To sum it up, ultrasound is now the method of choice when measuring post-void residual. Since it is an indirect form of measurement, one has to resort to mathematical formulae to be able to calculate the value of PVR. However, since the bladder does not always assume any particular geometrical shape, we have to be aware that, whatever model we use, we are prone to some degree of error. As always with models, really.

In the meantime: <strong>PVR</strong> (in mL) <strong>= Height</strong> (in cm ) <strong>x Width</strong> (in cm) <strong>x Depth</strong> (in cm) <strong>x 0.7</strong>

<em><strong>List of references:</strong></em>
<ul>
	<li>015/055 – S2k-Leitlinie: Sonographie im Rahmen der urogynäkologischen Diagnostik, Deutsche Gesellschaft für Gynäkologie und Geburtshilfe e.V., 2013</li>
	<li>Birch <em>et al</em>, “Serial Residual Volumes in Men with Prostatic Hypertrophy”, <i>British</i> <i>Journal</i> <i>Of</i> <i>Urology</i><i>, </i>1988.</li>
	<li>Lucas <i>et al., </i>“Guidelines on Urinary Incontinence“, European Association of Urology, 2015.</li>
	<li>Reynard <em>et al</em>, <em>Oxford Handbook of Urology, </em>3rd edition, Oxford Medical Publications, 2013.</li>
	<li>Simforoosh <i>et</i><i> al</i>., “Accuracy of residual urine measurement in men: comparison between real-time ultrasonography and catheterization”, <i>The Journal Of Urology</i>, 1997.</li>
</ul>
 
