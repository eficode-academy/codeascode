## Exercise 3 - Set up a simple build and test job for the application

### Configure a simple build job

Hint: We obviously want to use our good friend Docker to build the go app, to avoid installing go-lang and other dependencies on our build server (or locally on the developers machine).

Luck is with you, as the gowebserver repo has a Dockerfile that will actualy build the webserver.

Try something like: `docker build .` as a starter. Consider tagging the image with a name so you can run it later.

You might also want to look at the `--no-cache` option ...

If you really get curious about how the Dockerfile works, ask google or your instructor.

Did we forget to mention that you might need `sudo` to run docker commands inside Jenkins? Can you figure out why?
