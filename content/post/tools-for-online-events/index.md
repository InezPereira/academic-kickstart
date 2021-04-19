+++
title = "Tools for Online Events"
subtitle = ""

# Add a summary to display on homepage (optional).
summary = ""

date = 2020-09-13T14:53:21+02:00
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

{{< tweet 1304448759460433920 >}}

This year's Computational Psychiatry Course (CPC) Zurich, like many other events all over the world, faced the challenge of moving to an online setting. Much in the spirit of [this post](https://medium.com/@kording/how-to-run-big-neuro-science-conferences-online-neuromatch-io-49c694c7e65d), I'll share here the combination of tools that was used and how useful they proved to be at the CPC Zurich 2020. All the materials from this year's and previous events can be found [here](https://www.translationalneuromodeling.org/cpcourse/). This year's video recordings can be found [here](https://video.ethz.ch/lectures/d-itet/2020/autumn/227-0971-00L.html).

# Webinar tool - Creating a focused environment
We used Zoom Webinar to broadcast the lectures. Our Zoom Webinar workflow included:
- **Participant Registration**: participants were asked to register for the webinar.
Using this feature of Zoom Webinar meant setting up one Webinar per day, which
forced participants and speakers to use different links for each day. A shoutout
to Zoom here: it would be great to be able to add a CSV of the registrants
to a recurring Zoom Webinar 😊.
- **Technical Checks**: checking for technical problems (*e.g.* faulty video
  sharing, poor audio) can be done in Zoom Webinar's Practise room, before
broadcasting. When these checks are done consistently, you avoid quite a few
live surprises 😉.
- **Chat options**: Participants had the opportunity to chat on Slack, and so the
chat on Zoom Webinar was disabled. This proved to have one major advantage: it made
chat an opt-in feature of the lectures, and not something that just came
with the tool used. This led to less distractions for the speakers and chairs, and
possibly for some attendees. In addition, this also meant that it was clear that
the Q&A tool was the tool to use to ask questions (no chat moderator hunting for questions needed!).
- **Q&A**: attendees posed their questions via de Q&A tool and were able to upvote
each other's enquiries. Added to this, the session chair would also curate the Q&A list
and sometimes combine related questions. Participants always posed a lot
of questions, and to not cut discussions short, they were invited to repost them
in the Slack Q&A channel. Speakers often answered further questions on Slack 💛.

# Promoting interactions
## Slack
Slack proved to be a great tool: it was a way of answering questions and
sharing resources in a manner that was visible to everyone. In addition, attendees
often supported each other by answering each other's questions! 😍
Besides the usual #general, #fun and #random channels, the following other channels were created:
- #q_and_a: this channel was extensively used to follow up on discussions held
during the webinar and also provided an opportunity for attendees to ask further questions.
- #resources: to refer to journal articles, books, videos, slides, links to open
source software packages... some speakers even provided extensive reading lists!
- #tutorial_helpdesk: support was provided via this channel for the tutorials
involving installation of software.
- #zoom: to discuss technical issues related to zoom. Attendees would use this
channel to report issues during the webinar (and sometimes even propose
solutions).
- #job_postings: self-descriptive 🙃
- #social: a space where attendees could introduce themselves and start discussions
that could followed up on in the Gather rooms (see below).

## Gather rooms
[Gather](https://gather.town/) is a new video chat platform with a Gameboy feel,
particularly interesting because it parts from traditional meeting-directed
software.
A user on Gather becomes a sprite that can move around in a pixel-arty virtual space. You
only get to hear and talk to someone once you have sufficiently approached them.
This is essential, because it enables users to form groups and have conversations
in parallel... like in real life, basically. And, like in real life, you can move
from one group to another and actually run into people you know.
Gather offers a set of maps you can use off the shelf. However, making your own
customized maps is not only easy, it's also a lot of fun!
Tutorials on how to do this can be found on [Gather's YouTube channel](https://www.youtube.com/channel/UCd4uhlois5n9k6fRuVwSCuA).
I personally use online tools such as [this platform](https://www.pixilart.com/)
to add more pixel art and nerdy references 🤓.

## Mind-matching
Also in the spirit of what has been done at other great events and conferences,
we used [freely available software](https://github.com/titipata/paper-reviewer-matcher),
coupled with input from our own 🧠s to match participants based on their research interests.
Mind-matchers could then contact each other and meet. Having been matched myself
at other events, I found mind-matching to be a great way to meet new people.
Specifically, because these meetings have to be planned and organized, I found that
these interactions were always very purposeful and focused. I had great conversations
and met super interesting people via mind-matching, and hope CPC Zurich attendees
did so too.
