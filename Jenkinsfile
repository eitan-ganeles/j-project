pipeline {
    agent any
    environment {
        IMAGE_NAME = "petclinic-app"
    }
    parameters {
        booleanParam(name: 'run_tests', defaultValue: true, description: 'Run all tests')
        string(name: 'branch', defaultValue: 'main', description: 'Branch to use for running jenkins pipeline')
    }
    stages {
        stage('Build') {

            steps {
                echo 'Building..'
                git(url: 'https://github.com/spring-projects/spring-petclinic.git',
                    branch: 'main')
                sh " ./mvnw clean compile "
            }

        }
        stage('Test') {
            when {
                expression { return params.run_tests }
            }

            steps {
                echo 'Testing..'
                sh "./mvnw test"
            }

            post {
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }
        stage('Package as docker') {
            steps {
                script {
                    sh "./mvnw package"
                    pet_clinic_img = docker.build("$IMAGE_NAME", "-f ./Dockerfile .")
                    echo "Build finished successfully"
               }
            }
        }
    }
}
