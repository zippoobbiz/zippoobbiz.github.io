---
title: Backup hexo and auto deploy with Jenkins
date: 2017-08-21 21:30:38
tags: [Hexo, Git]
categories: [Ops, Jenkins]
---

![hexo](https://philsblog.b-cdn.net/images/hexo.png "hexo")
Finaly, I am able to update the blog again. I was trying to back up the whole project of the hexo blog and messed up......
I guess it's easier for you to watch other people's experience rather than do it your self.

Hexo only deploy the generated html files, however if you want start over after you computer crashed, or you wanted to write something on a different machine, it will be impossible unless you copy all of your existing work and write them again. So I started to backup everything. Here is how I did, just in case I forget.

1 Clone the deplyed project to a new folder
2 Create and checkout to a new branch
3 Git **rm** everything
4 Copy **config.yml**, **themes/**, **source**, **scffolds**, **package.json**, **.gitignore** to this new folder
5 Remove the **.git** and **.gitignore** from your themes folder
6 Git **add** all of the copied files and folders, **commit** and **push**

At this stage, you will be able to 
1) backup the project by **git add commit and push** in the new branch, 
2) and deploy hexo by **hexo clean generate deploy** to the old branch. 

But it takes two steps! We lazy people move the world forward, right? So I'd like to use jenkins deploy it for me!

So you need a Linux environment with **git npm hexo-cli hexo-server** installed and **ssh key** setup for github, then:

1 Download the war version of jenkins
2 run it `java -jar jenkins.war &> somelogs &`
3 Install all default plugins and also install github intigration(we use this one for webhook, it was called GitHub plugin, however it chaged to github intigration when I install it, who knows what it will be called when you install)

![github-plugin](https://philsblog.b-cdn.net/images/github-plugin.jpg "github-plugin")

4 Setup the **build** on jenkins, add your repo, choose the new branch we just created.
5 Add trigger

![jenkins](https://philsblog.b-cdn.net/images/jenkins-trigger.jpeg "jenkins")

6 Add Webhook on you github repo(go to that repo's settings)

![github-webhook](https://philsblog.b-cdn.net/images/github-webhook.jpeg "github-webhook")

7 Add the following cmd to your **build**
```bash
npm -v
rm -rf node_modules/
npm install
hexo clean
hexo generate
hexo deploy
```

You should be good by now, when you do a push something to the new branch, jenkins will pull you changes, build, and deploy it to github pages for you!

Don't forget add ssh key to ssh-agent and make sure the npm version is correct.

Have fun, happing blogging