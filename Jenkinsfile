pipeline {
    agent {
        label 'docker'
    }
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
// todo -erase!!
//                 sh """
//                  git clone https://github.com/spring-projects/spring-petclinic.git
//                  cd spring-petclinic
//                 """
            }
        }
        stage('Test') {
            when {
                expression { return params.run_tests }
            }
            steps {
                echo 'Testing..'
            }
        }
        stage('Package as docker') {
            steps {
                script {
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
