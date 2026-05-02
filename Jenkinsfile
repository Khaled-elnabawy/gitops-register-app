pipeline {
    agent { label "Jenkins-agent" }

    environment {
        APP_NAME = "register-app-pipeline"
        DOCKER_USER = "khaledelnabawy1"
        RELEASE = "1.0.0"
        IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"
    }

    stages {

        stage("Cleanup Workspace") {
            steps {
                cleanWs()
            }
        }

        stage("Checkout from SCM") {
            steps {
                git branch: 'main',
                credentialsId: 'github',
                url: 'https://github.com/Khaled-elnabawy/gitops-register-app'
            }
        }

        stage("Update the Deployment Tags") {
            steps {
                sh """
                   echo "Before update:"
                   cat deployment.yaml

                   sed -i 's|image:.*|image: ${DOCKER_USER}/${APP_NAME}:${IMAGE_TAG}|g' deployment.yaml

                   echo "After update:"
                   cat deployment.yaml
                """
            }
        }

        stage("Push the changed deployment file to Git") {
            steps {
                sh """
                   git config --global user.name "khaledelnabawy1"
                   git config --global user.email "khaledelnabawy@gmail.com"

                   git add deployment.yaml

                   git commit -m "Updated Deployment Manifest to ${IMAGE_TAG}" || echo "No changes to commit"
                """
                withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
                    sh "git push https://github.com/Khaled-elnabawy/gitops-register-app main"
                }
            }
        }
    }
}
