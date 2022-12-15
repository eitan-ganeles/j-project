# JFrog Task #
Jenkins Pipeline that downloads, compiles, tests, and builds the [pet clinic app](https://github.com/spring-projects/spring-petclinic)   

### Prerequisites
In order to run this pipeline, there is a need for:
1. Access to a Jenkins application [Download Jenkins](https://www.jenkins.io/download/).
2. There are 2 necessary plugins to add to jenkins: [Docker](https://plugins.jenkins.io/docker-workflow/) and [Git](https://plugins.jenkins.io/git/)

### How to set up the pipeline:
* Create a new Item in the jenkins UI
* Enter a name you prefer, and choose "Pipeline" type.
* In the configuration section, skip to the Pipeline section, and choose "Pipeline script from SCM" and enter the following:
    1. SCM: Git
    2. Repository URL: https://github.com/eitan-ganeles/j-project.git (The repo is public so no need for credentials)
    3. Branch Specifier: "*/${branch}" (this will take the branch from the parameter)
    4. Script Path: Jenkinsfile
* Run the pipeline :) 

### Pipeline Steps
There are 3 steps:
1. Compile - in this step the source code is downloaded directly from git, and compiled using the mvnw executable
2. Test - test the compiled code. A "Test Result" reporting all tests that were run
 should be available on the left hand menu after the job is finished.
3. Package - packages the project as a runnable Docker image. This stage builds the file named `./Dockerfile`.

### Pipeline Parameters
1. run_tests - set to False if you want to skip the testing stage.
2. branch - the branch in the j-project repo the Jenkinsfile should be taken from.  

### Docker 
In order to run the docker image that was build run from command line:
`docker run --publish 8080:8080 petclinic-image`
