---
layout: post
title: "Continuous Integration"
date: 2019-10-28 15:00:00 -5000
image: gitlab/title.png
tags: [Tutorial, Gitlab]
categories: [Tutorial, Gitlab]
---

One tool that can be useful for developers is continuous integration (CI) as it allows them to keep building their application then easily deploy a working version the has been tested. There are many CI services out there such as Travis-CI, CircleCI, CodeShip, and Jenkins. Git providers have started to build their own right into their products. Github has their own called actions and both BitBucket and Gitlab call their pipelines. Even AWS and Azure now have created CI services such as AWS CodeBuild and Azure DevOps.  

CI solutions can be very helpful where you are making a big program and want to make sure it passes a lot of tests or a simple program, but still, want to make sure that your program works well. It also helps with collaboration because you can have developers around the globe push their code to a repository which has CI implemented and you can see if it builds and passes tests correctly and not just on one person's machine. I have found a great use for using CI services with my own repositories.  

I started out with CI with BitBucket because it was there was good documentation to get started and they had items call pipes that were prebuilt to deploy code. The first pipeline that I built was for this blog as it uses Jekyll so it has to be built any time I want to view the HTML of it. It was a quick and simple pipeline that built it then deployed it with SCP to my server. The pipeline has since been removed but if you want to go back in the commit history for my blog you can find it (or just click [here](/other-files/CI/bitbucket-pipeline.yml.txt)). Since then I have moved on to Gitlab CI, which I am very happy with. Additionally, I have done some work with Travis-CI and Github Actions as well as built pipelines for my portfolio website and numerous other projects.  

Recently one of my projects optimizing my pipeline for my [portfolio website](https://gitlab.com/jwhite1st/Portfolio-Website), before it would take 5 minutes to deploy to my development server and something almost 7 minutes to fully run. Some of the issues that I found were taking time was all the script runs. Before I was using basic docker images and then installing the packages that I needed to complete my tests. My first fully complete pipeline took 9 minutes to run. How I optimized was switching from the normal docker images to customized ones. Before my production deployment was running on the npm docker image then installing firebase. Now I use a docker image that has firebase already install and only run an update command to make sure it is up to date. A couple days ago I just finished rolling out my own docker image to use html5validator against my HTML and CSS code. This involved working on the python package ([html5validator](https://github.com/svenkreiss/html5validator)) that had not been updated in a while and fixing those errors and after completing that I created my own docker image, available [here](https://cloud.docker.com/repository/docker/jwhite1st/html5validator/general), which gets all the required packages that I need. This was around two weeks of off and on development in various areas. I am very happy with the results because the entire pipeline completes in just 3 minutes and 30 seconds and 4 minutes if firebase requires an update, which is nearly a third of the time that it took from the first complete pipeline, the newest CI configuration is available [here](https://gitlab.com/jwhite1st/Portfolio-Website/blob/master/.gitlab-ci.yml).  

In conclusion, Continuous integration is a great service to use because it allows for easier automation for programs. Gitlab allows you to schedule a pipeline as well. My blog is rebuilt and deployed every day around 4 pm UTC. If you want to see when this version was deployed then inspect the element and look in the head section and you will a "Built" tag which shows the time this site was built. This feature allows me to schedule blog posts as I can write them in advance then set the publish date in the future and once it is past the time the post will be included. I encourage you to find out how you can use CI services with your repositories.