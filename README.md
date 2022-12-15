# JFrog Task #
Jenkins Pipeline that downloads, compiles, tests, and builds the [pet clinic app](https://github.com/spring-projects/spring-petclinic)   

### Prerequisites
In order to run this pipeline, there is a need for:
1. Access to a Jenkins application [Download Jenkins](https://www.jenkins.io/download/).
2. There are 2 necessary plugins to add to jenkins: [Docker](https://plugins.jenkins.io/docker-workflow/) and [Git](https://plugins.jenkins.io/git/)

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
