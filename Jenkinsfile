pipeline {
    agent any

  stages {
        stage('Build') {
            steps {
                echo 'Building.. attempt 2'
                git(url: 'https://github.com/spring-projects/spring-petclinic.git',
                    branch: 'main')
//                 sh """
//                  git clone https://github.com/spring-projects/spring-petclinic.git
//                  cd spring-petclinic
//                 """
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
            }
        }
        stage('Package as docker') {
            steps {
                sh """
                    docker build --tag petclinic-app .
                """
            }
        }
    }

}
