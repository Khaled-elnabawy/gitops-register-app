pipeline {
    agent { label "Jenkins-agent" }

    environment {
        APP_NAME = "register-app-pipeline"
        DOCKER_USER = "khaledelnabawy1"
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

                   # Ensure image is always set to latest
                   sed -i 's|image:.*|image: ${DOCKER_USER}/${APP_NAME}:latest|g' deployment.yaml

                   # Update the build annotation so ArgoCD detects a real change in git
                   sed -i 's|build-number:.*|build-number: "${BUILD_NUMBER}"|g' deployment.yaml

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

                   git commit -m "Updated Deployment Manifest - Build #${BUILD_NUMBER}" || echo "No changes to commit"
                """
                withCredentials([gitUsernamePassword(credentialsId: 'github', gitToolName: 'Default')]) {
                    sh "git push https://github.com/Khaled-elnabawy/gitops-register-app main"
                }
            }
        }
    }
}

