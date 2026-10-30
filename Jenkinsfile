pipeline{
    agent {
        node {
            label 'agent-1'
        }
    }

    options {
        timeout(time: 10, unit: 'MINUTES')
        disableConcurrentBuilds()
    }
    environment {
        COURSE = 'Jenkins'
        ACCOUNT_ID = '143710972330'
        PROJECT = 'roboshop'
        COMPONENT = 'catalogue'
    }


    stages{
        stage('Read Version') {
            steps {
                script {
                    def packageJson = readJSON file: 'package.json'
                    appVersion = packageJson.version
                    echo  "Application Version: ${appVersion}"
                }
            }
        }
        stage("Install Dependencies") {
            steps{
                script {
                    sh """
                        npm install
                    """
                }
            }
        }
        stage("check docker") {
            steps{
                sh """
                    whoami 
                    id
                    docker --version
                    docker ps
                """
            }
        }

        stage("Build Image") {
            steps{
                script {
                  withAWS(region:'ap-southeast-2',credentials:'AWS-Creds'){
                        sh """
                            aws ecr get-login-password --region ap-southeast-2 | docker login --username AWS --password-stdin ${ACCOUNT_ID}.dkr.ecr.ap-southeast-2.amazonaws.com

                            docker build ${ACCOUNT_ID}.dkr.ecr.ap-southeast-2.amazonaws.com/${PROJECT}/${COMPONENT}:latest 

                            docker images
                            
                            docker push ${ACCOUNT_ID}.dkr.ecr.ap-southeast-2.amazonaws.com/${PROJECT}/${COMPONENT}:${appVersion}

                        """
                    }
                }
            }
        }
    }
    post {
        success {
            echo "Build succeeded!"
        }
        failure {
            echo "Build failed!"
        }
        aborted {
            echo "Build aborted!"
        }
    }
}





