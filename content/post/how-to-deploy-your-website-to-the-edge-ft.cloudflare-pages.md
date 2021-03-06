+++
authors = ["Josh Powell"]
date = 2021-04-12T15:00:00Z
draft = true
excerpt = "Running your website in 200+ locations has never been so easy!"
hero = "/images/how-to-deploy-to-the-edge-pages-hero.png"
title = "How to deploy your website to the edge! Ft. Cloudflare Pages"

+++
This week Cloudflare have [announced ](https://blog.cloudflare.com/cloudflare-pages-ga/)that Pages, there Serverless webpage hosting service will be exiting beta and move to general release! So I thought it was about time I made a blog post on how to setup and deploy them!

### Requirements

To setup a website on Cloudflare Pages you'll needed the following:

* A [GitHub](https://github.com/) account (other source controls are currently not supported)
* A [Cloudflare](https://cloudflare.com) account (you don't even require a domain! but I highly recommend you do)

### 1. Create a Git repository

To start the deployment of your first page, your going to need a Git repository that Cloudflare can download and build your project from.

If you head to [github.com](https://github.com) and in the top right hand corner click the little plus button, then click "New repository". ![GitHub new repository ](https://share.hoedab.tech/21/04/chrome_Wf31SIcpc8.png)

On the next page you'll need to specify a couple things;

The repository name is the first thing you need to specify. I tend to name all of my repositories after the URL they will be deployed too, such as blog-joshua-wales or hoedab-tech.

The next field is the description, this is completely optional.

You next have to specify weather you want the project to be open to everyone, or private. I personally like to keep most of my repositories private, but this comes down to preference.

There is no need to add a README / .gitignore / licence for the purposes of getting us setup for Cloudflare pages.

[//]: <> (https://share.hoedab.tech/21/04/chrome_S08vOm8aPK.png)

### 2. Commit & Push your website

Now that you've made your repository, your going to have to upload your website to the repository which will link up with Cloudflare.  I personally a piece of software called [Gitkraken](gitkraken.com) but GitHub have their own desktop app which you can download [here.](https://desktop.github.com/ "Github Desktop")

Once you've signed in, your going to have to clone the repository locally and then copy and paste your website files into it.

### 3. Login to Cloudflare

### 4. Configure Pages

### 5. Create your first Cloudflare Page!

### 6. Custom tweaks

Now there are a couple tweaks that you can apply to your workers site to make it perform that little better and more security but aren't critical to your basic Cloudflare page.

#### Page rules

#### Custom HTTP headers via Workers

Unlike your own webserver, you can't simply edit the header config on a Cloudflare page so you will need to deploy the following script on a Worker to achieve an A+ on [securityheaders.com](https://Securityheaders.com)
{{< centre >}}
{{< workers-headers-code >}}
{{< /centre >}}