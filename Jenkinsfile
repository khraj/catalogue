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



