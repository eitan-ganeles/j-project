pipeline {
    agent any
    environment {
        IMAGE_NAME = "petclinic-image"
    }
    parameters {
        booleanParam(name: 'run_tests', defaultValue: true, description: 'Run all tests')
        booleanParam(name: 'push_image', defaultValue: false, description: 'Push image to repo')
        string(name: 'tag_image', defaultValue: '', description: 'Add a specific tag to the build')
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
                    sh "pwd; ls;"
                    image_name = "$IMAGE_NAME"
                    if (params.tag_image != '') {
                        image_name += ":${params.tag_image}"
                    }

                    pet_clinic_img = docker.build("${image_name}", "-f ./Dockerfile")
                    echo "Build finished successfully"

                    if (params.push_image) {
                        "Pushing image..."
                        pet_clinic_img.push()
                    }
    //                 sh """
    //                     docker build --tag petclinic-app .
    //                 """
               }
            }
        }
    }

}
