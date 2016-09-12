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

 * Can you write true unit tests instead of functional http tests?
 * Can you find a way of splitting up your tests, so that you can control when to run unit tests and when to run http tests?


## Optional tasks to keep you going
### Writing jobDSL
 * Try to re-create one or more of your build jobs using JobDSL.
 * Try to use jobDSL to set up a Jenkins "Pipeline View" to show your pipeline status.

## Using the provided JobDSL and analyzing the created pipeline.
 * The go webserver actually has a JobDSL script that sets up a pipeline for the project. Try to get it running in a seed job that polls for changes.
 * Experiment with making simple iterative changes to the pipeline and see the seed job recreate the generated jobs.
 * Try to understand all the things that the pipeline steps do to pass parameters on to the downstream jobs.
