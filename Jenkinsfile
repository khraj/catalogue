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

        stage("Build Image") {
            steps{
                script {
                    sh """
                        docker build -t catalogue:${appVersion} .
                    """
                }
            }
        }

        stage('Test') {
            steps {
                       echo "Testing..."                                
            }
        }
    
        stage('Deploy') {
            steps {
                echo "hello Nice to meet you...!!"
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
    }
    post {
        always {
            echo "Cleaning up..."
            cleanWs()
        }
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





