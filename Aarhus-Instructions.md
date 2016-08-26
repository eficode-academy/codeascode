# Continuous Delivery Pipeline - The Project

This group project should take you through most of the steps for setting up a functional pipeline for your own project. In this project we have a very small product, a tiny webservice implemented in GO - converting integers to their Roman numeral representation.

A pipeline for this small project could contain steps like the following:

 * Build 
 * Some sort of quick ‘Unit’ test
 * Deploy to a test environment
 * Functional tests
 * Release
 * Deploy to production

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

The project is done in groups, and we will pause you all every now and then to give some feedback during the day, and to enable you to share experiences. You will have all day to work with the project, and we do not have a definitive "DONE" criteria, so just take the time you need to understand the steps in the build pipeline.

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

We use Kanban boards hosted by (waffle.io) which will be introduced in preparations below.

## Preparations

Each team needs _one_ server to be their pipeline server.
Make sure that everyone connects to that particular server when setting things up.


The starting point for the project is Go:[https://github.com/praqma-training/gowebserver](https://github.com/praqma-training/gowebserver).

   1. **Make a fork for your team**. Fork the project in github to make the shared repository for your team. Add the teammates as collaborators
   2. Enable github issues
   3. Create board at waffle.io

This will serve as the basis for your work, and should be up to date at all times. When you have created the waffle board, send a link to #aarhus on slack.

## Step I
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

## Step II - Set up initial build and test jobs for the application

### Configure a simple build job

Hint: We obviously want to use our good friend Docker to build the go app, so that we avoid installing go-lang and other dependencies on our build server (or locally on the developers machine).

Luck is with you, as the gowebserver repo has a Dockerfile that will actualy build the webserver. 

Try something like: `docker build .` as a starter. Consider tagging the image with a name so you can run it later.

You might also want to look at the --no-cache option ...

If you really get curious about how the Dockerfile works, ask google or your instructor.

### Setup your build job to poll Github for changes.

### Set up simple testing
Make your job run the "unit tests" as well. (yes, we know that the included tests are functional tests. Feel free to write some true unit tests as well).

Hint: The docker image you built has go installed, and go allows you to use the command `go test` to 
automatically run any tests that follow the `func TestXxx(*testing.T)` signature. Again no need to install any dependencies,
just use the image you just built.

When you get this far, you are ready to start TDD'ing your web app.

## Step III - pretested 
Implement a Pretested Integration workflow

Add [pre-tested integration](https://wiki.jenkins-ci.org/display/JENKINS/Pretested+Integration+Plugin) for your build.

Hint: Since Jenkins might have to do commits on merges, you will have to set up a user.name and user.email setting in Jenkins global configuration. ("jenkins" and "jenkins@localhost" should do fine for now).

## Step IV - start implementing Roman Numerals

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

Do some work on implementing the Roman Numerals converter, to see the build pipeline in action. Help for the Go-lang syntax can be found here: [Effective GO](https://golang.org/doc/effective_go.html)

Don't focus on using fancy language constructs or using a fancy algorithm. The actual coding exercise is not important - instead focus on the process of making small incremental changes, commiting and pushing them, and see how the Continuous Delivery Pipeline works. 




## Step V 
Setup performance test

## Step VI - Extend your pipeline
Now that we have a basic pretested integration setup that only allows "good" commits on master, it is time to continue the CD storyline and add other verification steps "post-integration".

Suggestions might include:

  * Run functional tests
  * Deploy your webapp "to a test environment", e.g. on port 8081.
  * Use the included Dockerized siege-engine tool to load test your application.
  * Can you find a simple code coverage tool for go or other static analysis?
  * Release notes?
  * Versioning?

If a commit passes through your pipeline and has "sufficient" quality, it is time to deploy it to production. E.g. port 80

## Step VII

Continue work on the roman numerals converter. If you have already completed the full converter, try to see if you can improve the way you test it. 

Ideas could be:

 * Can you write plain true unit tests instead of functional http tests?
 * Can you find a way of splitting up your tests, so that you can control when to run unit tests and when to run http tests?


## Optional tasks to keep you going
### Writing jobDSL
 * Try to re-create one or more of your build jobs using JobDSL. 
 * Try to use jobDSL to set up a Jenkins "Pipeline View" to show your pipeline status.

## Using the provided JobDSL and analysing the created pipeline.
 * The gowebserver actually has a JobDSL script that sets up a pipeline for the project. Try to get it running in a seed job that polls for changes.
 * Experiment with making simple iterative changes to the pipeline and see the seed job recreate the generated jobs.
 * Try to understand all the weird things that the pipeline steps do to pass parameters on to the downstream jobs.
