pipeline {
    agent { label "Jenkins-agent" }

    environment {
        APP_NAME = "register-app-pipeline"
        DOCKER_USER = "khaledelnabawy1"
        IMAGE_TAG = "${BUILD_NUMBER}"
    }

    stages {

        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }

        stage("Checkout from SCM") {
            steps {
                git branch: 'main', credentialsId: 'github', url: 'https://github.com/Khaled-elnabawy/gitops-register-app'
            }
        }

        stage("Update the Deployment Tags") {
            steps {
                sh """
                   sed -i 's|image:.*|image: ${DOCKER_USER}/${APP_NAME}:${IMAGE_TAG}|g' deployment.yaml
                   cat deployment.yaml
                """
            }
        }

        stage("Push the changed deployment file to Git") {
            steps {
                sh """
                   git config --global user.name "khaled-elnabawy"
                   git config --global user.email "khaledelnabawy@gmail.com"
                   git add deployment.yaml
                   git commit -m "Updated Deployment Manifest"
                """
                withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
                    sh "git push https://github.com/Khaled-elnabawy/gitops-register-app main"
                }
            }
        }
    }
}
