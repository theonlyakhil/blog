---
title:  "My Take On DevOps"
search: true
categories:
  - DevOps 
last_modified_at: 2018-10-17T08:05:34-05:00
header:
  teaser: /assets/images/blog/my-take-on-devops/devops-cover.png
---
![DevOps](/assets/images/blog/my-take-on-devops/devops-cover.png)

## What is DevOps?

I heard this term first when I was doing my internship at Appfabs. They focused on DevSecOps as they were a Security based company. So, to understand DevSecOps, I had to know what is DevOps. The first thing I was told that DevOps is a methodology, not a technology. DevOps is a methodology used in SDLC (Software Development Life Cycle) where the development team and operations team work together from designing stage to production support. To understand DevOps and why DevOps was introduced, we need to know the methods used before DevOps was introduced. 

All these started when the waterfall model was introduced into SDLC. This model was best suited when:-
1. The product requirements are clear and fixed.
2. The product definition is stable. That is, the product's client has a clear cut idea on how the product must be.
3. The project has very least risk during development.

The main disadvantages using this method was:-
1. It was slow.
2. Change implement was slow.

As in software field, slow means loss. Using this method in huge and sensitive projects gave companies huge losses.
Keeping the disadvantages in mind, a new model was introduced that could fix all the disadvantages of the waterfall model. Thus, came the Agile methodology.
Agile methodology brought continuous iteration in product development and testing throughout the SDLC. 

The Agile methodology is bested when:-
1. The product requirements frequently change.
2. The product requires faster development.

And guess what? even this method didn't work out for many companies, due to:-
1. Lack of agility in the operations phase of the product lifecycle.
2. The issue in the code environment. That is, the code works perfectly fine in developer's PC, but won't work on the production environment (Server).
3. The deployment of the product is linear.

To solve the disadvantages in agile methodology, the DevOps was introduced. The DevOps was best suited when:-
1. The product's requirement changed frequently.
2. When the Operations team needs to become agile.
3. For bridging the gap between the development team and the operations team.

To understand DevOps better, we will learn a case study of a big shot company like Facebook who finally used DevOps due to their product's need. In 2011, Facebook introduced a major update that includes many cool features like timeline support, music support and many more. The public was notified about this new release. As Facebook as a huge hit during that time, all the active Facebook users (almost 500 million) started using Facebook to use these features. As Facebook's servers during that time were not prepared to handle this huge traffic, it got shut down causing a server meltdown. Added to this major issue, the new features got a mixed opinion among the users. That is, many users loved it, other users absolutely hated it and few requested for modification. These kinds of reaction created a chaotic situation in Facebook headquarters. To solve this issue, they brought in DevOps and introduced a technique called "Dark Launching". The "Dark Launching" is a type of product release technique in which:-
1. New features will be first released to a smaller group of users (mainly internal BETA testers). There will be constant communication between the team and the BETA testers. The communication involves taking feedback and other techniques that help to improve the features to the user's need. 
2. When the team gets an assurance that the features can be released to the public, they release it to public BETA and then to the public through multiple product releases.

![Facebook dark launching](/assets/images/blog/my-take-on-devops/devops-fb-example.png)

Facebook achieves "Dark Launching" via the use of the delivery pipeline. A delivery pipeline is a set of steps that a code goes through till it reached production. A pipeline contains an automated building, testing and deploying tools that work together till the product's release.

So after learning a case, we can say that "DevOps is a software development approach that involves continuous development, testing, integration, deployment and monitoring throughout the development cycle." 

## DevOps Lifecycles

The lifecycle represents the stages in DevOps:-
1. Continuous Development: The continuous development involves the product's development is split into smaller development cycles. 
2. Continuous Testing: This cycle involves the Quality Assurance team identifying any bugs or errors in the code after every development cycle.
3. Continuous Integration: This cycle involves integrating the new code with the existing code present in the production environment.
4. Continuous Deployment: This cycle involves the deployment of code into the environment. The deployment is done in such a way that, it doesn't affect the product's current network traffic.
5. Continuous Monitoring: The monitoring helps the team to monitor changes in the application after every lifecycle.

## DevOps Tools

![DevOps tools from edureka](/assets/images/blog/my-take-on-devops/devops-tools.png)

The main advantage that DevOps gave us is "Automation". The developer can automate the whole operations process in the software lifecycle. Automation in DevOps is achieved using tools at different stages of its cycle.
The following tools (that I have used) are used at different stages:-
1. Plan - Jira
2. Code - Git
3. Build - Gradle, Maven
4. Test - Selenium, JUnit
5. Integrate - Jenkins
6. Deploy - Docker
7. Operate - Ansible
8. Monitor - Nagios, slack

Let's consider an example of a company that has implemented DevOps methodology in their product and have used few tools for automation. The tool Jenkins (integration tool) detects changes in code and automatically triggers a build using tools like Gradle or Maven. After the build, Jenkins will deploy the code for testing. The testing is done by test tools like Selenium (if web app), JUnit (For Java apps) or any other testing tool. The deployment is handled using Docker. The running code is then monitored by tools like Nagios, Splunk or ELK Slack.

