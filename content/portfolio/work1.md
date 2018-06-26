+++
showonlyimage = false
draft = false
image = "img/portfolio/hugologo.png"
date = "2018-06-26T00:12:00-07:00"
title = "Making a blog with Hugo"
weight = 0
+++

I decided that, in the interest of documenting my projects, my first post should start from the beginning.

What follows is an overview of how this blog was made using Hugo - a static website generator that I've never used before today.
<!--more-->

## Why not just make a WordPress page like a normal person?

Good question.

It's my philosophy that, as a general rule, every tech project should begin with an evaluation of the potential options. When planning a project, it's tempting to just go straight to what you know and are familiar with - but oftentimes, the tool you know isn't the best tool for the job.

WordPress is probably the most widely used framework for simple small scale websites, and most people (myself included) have lots of experience in using it. This can actually be a big advantage, as there's a plethora of resources available for making WordPress sites - tutorials, themes, plugins, you name it.

Hugo, on the other hand, is a static content generation framework. The big advantage of Hugo is that you run it once, generate some static HTML files, and then serve those files. Since everything is generated beforehand, your site can be served from something like Google Cloud Platform's Cloud Storage Buckets.

This is a *massive* advantage in a few arenas. 

First, it's cheap. You don't even have to run a server, since GCS can serve up your content directly to users. You're only charged for the amount of data you serve, not the overhead of running a LAMP stack on a virtual machine instance.

Second, it's *fast*. The page loads as quickly as you can download it from Google's GCS servers. Since GCS buckets can be made multi-regional, users can get that content from whatever backend storage facility is geographically closest to them. In addition, this also takes advantage of Google's edge network and CDN, giving you things like content chaching for *even faster* performance.

Third, it's scalable. GCS buckets are designed to be capable of handling large amounts of traffic. It doesn't matter if one person is viewing the site, or if a million people are viewing the site - GCS can handle it. All the serving backend is Google managed, so I don't ever have to worry about things like autoscaling, mirroring, and load balancing. I just throw the files up and let Google handle the rest. This is called "no-ops" and it's fantastic.

To me, these benefits were well worth the trouble of learning a new framework. And I've been meaning to get more practice with Go anyway, so I figured I'd give it a shot.

## So how is it done?

Installing Hugo was, in typical linux fashion, absurdly easy. You just type:

>sudo apt install hugo

...and that's it.

Getting the website together was a little more complicated. For that I had to cd into my home directory and run the command:

>hugo new site AboutTwoMonths

...which set up the base directories to run the site. I also initialized a Git repo with:

>cd AboutTwoMonths

>git init;

...although I don't think that's strictly necessary, it's a good thing to have. After that I went ahead and browsed what themes were available, and settled on this one, the "Creative Portfolio" theme. Installing it was pretty straightforward:

>cd themes
>git clone https://github.com/kishaningithub/hugo-creative-portfolio-theme.git

The Creative Portfolio theme comes with a prebuild example site, which serves as a good jumping off point for making your own site. I went ahead and copied the example site over with:

>cd ..

>cp themes/hugo-creative-portfolio-theme/exampleSite/* .

With everything in place, I went ahead and started the server with:

>hugo server

And that's it! The site was up and running on my local machine.

I did a little housecleaning in between there, getting rid of unneeded files and whatnot - like the git file that was created when I cloned the theme from the github repo. But that's the basics right there. Right now, as I type this, the server is running on my local machine, and monitoring for any changes in the content files of my project. For this post I just modified one of the example pages. It's actually very nice, because the hugo server automatically recognizes any changes I make and immediately updates the site. It's almost as easy as WYSIWYG, all I have to do is hit "save" and then switch over to my browser to see the changes reflect.

I suspect I'll make another post about working with Hugo once this site is a little further along, to go over the process for exporting static site files and hosting them on GCS. But so far, so good. Stay tuned for updates!

-- Theo