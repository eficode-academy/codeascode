## Jenkins jobs as code

Now we will use the jobDSL defined in the go-roman git repository.

- Create a "Seed" job (freestyle) and provide the below string params:
    DOCKER_USERNAME & GITHUB_USERNAME
- Add your go-roman fork git details
- Add a build step to "Process Job DSL's"
- Save the job configuration
- Run the job, giving your github and docker hub username
- Verify that the generated pipeline can execute correctly
