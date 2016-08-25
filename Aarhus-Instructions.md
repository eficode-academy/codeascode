# Continuous Delivery Pipeline - The Project

This group project should take you through most of the steps for setting up a functional pipeline for your own project. In this project we have a very small product, a tiny webservice implemented in GO - converting integers to their Roman numeral representation.

When the day is over you should be able to make changes to your Roman numeral implementation and follow the build steps all the way to a new release.

We want to use all the tools and techniques we learned this week.  

 * Test driven development
 * Agile task management with github issues
 * Version control with git
 * Build, test and ship with docker containers
 * Continuous Delivery with Jenkins
 * Extra credit:
   * Implement the praqmatic git flow branching strategy

## Outline of the day

The project is done in groups, and we will pause you all every now and then to give some feedback during the day, and to enable you to share experiences. You will have all day to work with the project, and we do not have a definitive "DONE" criteria, so just take you time you need to understand the steps in the build pipeline.

The end goal for our development process:

 * A build and test environment with docker for developers
 * Have a jenkins server set up to automatically build `master` branches
 * Automatically delivering successful builds to the production environment
 * Configure the Jenkins jobs using JobDSL and Groovy

Every iteration is devided into the following sections:
   * **Planning**: create the github issues to describe the work you will do
   * **Working**: working on the sprint items
   * **Demo**: show what was done
   * **Retrospective**: reflect on how it went and decide on ways to improve

We use Kanban boards hosted by (waffle.io) which will be introduced in iteration one.

## Preparations

Each team needs _one_ server to be their pipeline server.
Make sure that everyone connects to that particular server when setting thing up.

Create a Kanban board for your project on [waffle.io](http://waffle.io). This will serve as the basis for your work, and should be up to date at all times. When you have created the waffle board send a link to 
** TODO MBA ** Where/how to expose the waffle board to instructors. MBA will write this.

## Iteration one
In order to build our pipeline, we need to have our CI infrastructure up and running.

### Setup the infrastructure
Clone our [code infrastructure repository](https://github.com/praqma-training/code-infra)
```
	git clone https://github.com/praqma-training/code-infra
	cd code-infra/containers
	sudo ./create-homes.sh
```

This reposiory has _a lot_ of containers that can be started, but we need only jenkins.
```
	cd jenkins
```
We need to build the docker image inside the jenkins folder, and then run it.

```
	docker build -t myjenkins .
	docker run -d -p 8081:8080 -p 50000:50000 -v /opt/containers/jenkins_home:/var/jenkins_home -v /var/run/docker.sock:/var/run/docker.sock -v /usr/lib/x86_64-linux-gnu/libapparmor.so.1.1.0:/lib/x86_64-linux-gnu/libapparmor.so.1 myjenkins
```

Check that the jenkins server is up and running on:
http://YOUR-AWS-INSTANCE:8081/jenkins

### Set up the build and test jobs for the application

The starting point for the project is Go:[https://github.com/praqma-training/gowebserver](https://github.com/praqma-training/gowebserver).

   1. **Make a fork for your team**. Fork the project in github to make the shared repository for your team. Add the teammates as collaborators
   2. Enable github issues

## The automation setup

### Configure the first build job

**TODO Johan** Instructions on setting up the build (and deploy?)

**TODO Johan** Instructions on running first build

**TODO** 

## Iteration two - Pretested Integration

Add [pre-tested integration](https://wiki.jenkins-ci.org/display/JENKINS/Pretested+Integration+Plugin) for your build.

## Iteration three - actually implement Roman Numerals

We need a `go` web service that when we hit the `/roman/<number>` url it will return the roman numeral representation of it.

````
Given a positive integer number (eg 42) determine
its Roman numeral representation as a String (eg "XLII").

You cannot write numerals like IM for 999.
Wikipedia states "Modern Roman numerals are written by
expressing each digit separately starting with the
leftmost digit and skipping any digit with a value of zero."

Examples:
1 ->    "I" | 10 ->    "X" | 100 ->    "C" | 1000 ->    "M"
2 ->   "II" | 20 ->   "XX" | 200 ->   "CC" | 2000 ->   "MM"
3 ->  "III" | 30 ->  "XXX" | 300 ->  "CCC" | 3000 ->  "MMM"
4 ->   "IV" | 40 ->   "XL" | 400 ->   "CD" | 4000 -> "MMMM"
5 ->    "V" | 50 ->    "L" | 500 ->    "D" |
6 ->   "VI" | 60 ->   "LX" | 600 ->   "DC" |
7 ->  "VII" | 70 ->  "LXX" | 700 ->  "DCC" |
8 -> "VIII" | 80 -> "LXXX" | 800 -> "DCCC" |
9 ->   "IX" | 90 ->   "XC" | 900 ->   "CM" |

1990 -> "MCMXC"  (1000 -> "M"  + 900 -> "CM" + 90 -> "XC")
2008 -> "MMVIII" (2000 -> "MM" + 8 -> "VIII")
  99 -> "XCIX"   (90 -> "XC" + 9 -> "IX")
  47 -> "XLVII"  (40 -> "XL" + 7 -> "VII")

````

Implement the Roman Numerals in the following ways, to see the build pipeline in action. Help for the GO syntax can be found here: [Effective GO](https://golang.org/doc/effective_go.html)

The important part is not to use fancy language constructs or optimize the algorithm, but to make different build and see how the Continuous Delivery Pipeline works. 

 * Naively
 * Iteratively
 * Recursively using switch cases [Go Language - Switch](https://golang.org/doc/effective_go.html#switch)


## Iteration four 
Setup performance test

## Iteration five
Setup your build job to poll Github for changes.


## Iteration six
Try to create the same build job using JobDSL
