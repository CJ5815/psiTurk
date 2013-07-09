
What is this?
============

PsiTurk is an open platform for conducting custom behvioral experiments on
Amazon's Mechanical Turk. 

It is intended to provide most of the backend machinery necessary to run your
experiment. It uses AMT's _External Question_ HIT type, meaning that you can
collect data using any website. As long as you can turn your experiment into a
website, you can run it with PsiTurk!

You can direct questions to our [Q&A Google group](https://groups.google.com/d/forum/psiturk).

Install
=======

The easiest way to install pip . At a terminal simply type:

    pip install git+git://github.com/NYUCCL/psiTurk.git@dev


Quick Start
===========

Once PsiTurk is installed, you'll need to set up your environment.

1. Sign up for an AWS account, available [here](http://aws.amazon.com/).
2. Sign up for a Mechanical Turk requester account, available
   [here](https://requester.mturk.com/).
3. In a terminal, install psiturk by typing `pip install
   git+git://github.com/NYUCCL/psiTurk.git@dev`.
3. To use our example experiment, check out the repository by typing `git clone
   git://github.com/NYUCCL/psiTurk.git` or download it [as a zip
   file](https://github.com/NYUCCL/psiTurk/archive/master.zip).  You can modify
   this experiment to create your own.
4. Move into the repository with `cd psiturk`.
5. Start the dashboard by typing `psiturk`. The dashboard should pop up in a browser window.
6. Enter your AWS account information under the "AWS Info" tag.

*Note*: If you are just testing the server without posting your HIT to Amazon,
you can see the experiment at the following link:
http://localhost:5001/mturk?assignmentId=debug&hitId=debug&workerId=debug


Experiment design
=================

We have provided an example stroop experiment that could form the basis of your
own experiment. The task logic is programmed in Javascript, which will run in
your participant's browser. Most of the code can be found in `static/task.js`.
It works by dynamically changing the html document served to participants in
`templates/exp.html` and communicating with the server code which can be found
in `psiturk/psiturk.py`. PsiTurk assigns a condition and counterbalance to each
participant. These are fed into JavaScript by plugging them into
`templates/exp.html`. PsiTurk actively manages the condition and counterbalance
subjects are assigned to, helping you fill them in evenly. To tell PsiTurk how
many conditions and counterbalance identities are possible in your experiment,
adust `num_conds` and `num_counters` in `config.txt`.

Deployment
==========

Configuration
------------
To make your experiment available on the internet, you will need to make the
following changes to the configuration file:

    host: 0.0.0.0
    question_url: http://yoururl:yourport/mturk

replacing `yoururl` with the url to your surver, and `yourport` with the port
you have configured in `config.txt` (by default, 5001).

Database
--------

We recommend using a deployment-robust database solution such as
[MySQL](http://www.mysql.org) or [PostgreSQL](http://www.postgresql.org).
SQLite does not allow concurrent access to the database, so if the locks work
properly, simultaneous access (say, from multiple users submitting their data
at the same time) could destabilize your database. In the worst (unlikely)
scenario, the database could become corrupted, resulting in data loss.

Instructions for setting up a MySQL server on a Mac can be found 
[in the wiki](https://github.com/NYUCCL/psiTurk/wiki/Macintosh-Configuration).
Other platforms, check out instructions at
[mysql.org](http://dev.mysql.com/doc/refman/5.5/en//installing.html).

FAQ
---

 * **I can't seem to get pip working**.  If you are having trouble setting up
   Python, we suggest installing the [Enthought Python
   Distribution](https://www.enthought.com/products/epd/), which is licensed
   for free to academics [at this
   link](https://www.enthought.com/products/canopy/academic/). It provides a
   kitchen-sink-included version of Python which includes `pip`.

Copyright
=========
You are welcome to use this code for personal or academic uses. If you fork,
please cite the authors (Todd Gureckis and John McDonnell).



