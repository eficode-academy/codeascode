## Exercise 3 - Set up a simple build and test job for the application

### 3.1 Configure a simple build job

Hint: We obviously want to use our good friend Docker to build the go app, to avoid installing go-lang and other dependencies on our build server (or locally on the developers machine).

Luck is with you, as the go-roman repo has a Dockerfile that will actualy build the webserver.

Try something like: `docker build .` as a starter. Consider tagging the image with a name so you can run it later.

You might also want to look at the `--no-cache` option ...

If you really get curious about how the Dockerfile works, ask google or your instructor.

Did we forget to mention that you might need `sudo` to run docker commands inside Jenkins? Can you figure out why?

If you need a shortcut, try running the `./build.sh` script for your build step...

### 3.2 Set up a test job

Now we want to add a second job to our pipeline.  Trigger the test job from the build job, and pass through the parameters in `props.env` together with `GITHUB_USERNAME` and `DOCKER_USERNAME`.

For the build step, execute `./test.sh`.  Can you create a change that would make it fail?

### 3.3 Extra-credit: can you set up automatic triggering from github?

It would be nice if we could automatically trigger our pipeline as soon as a new commit arrives.  Take a look at github webhooks and see if you can make the integration work.
