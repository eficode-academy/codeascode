## Step III - pretested
Implement a Pretested Integration workflow

You should have the [pre-tested integration plugin](https://wiki.jenkins-ci.org/display/JENKINS/Pretested+Integration+Plugin) installed on your jenkins.

Add a new job to the jobDSL definition to merge "deliver" branches into master if the build step passes.

Hint: Since Jenkins might have to do commits on merges, you will have to set up a `user.name` and `user.email` setting in Jenkins global configuration. ("jenkins" and "jenkins@localhost" should do fine for now).

Verify that bad revisions are rejected and good revisions are merged.
