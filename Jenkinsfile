pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                script {
                    killOldBuild()
                }

                echo 'Building..'
                sh 'javac *.java'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                sh 'java helloworld'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
    post {
        always {
            echo 'One way or another, I have finished'
        }
        success {
            echo 'I succeeded!'
        }
        unstable {
            echo 'I am unstable :-('
        }
        failure {
            echo 'I failed :('
        }
        changed {
            echo 'Things were different before...'
        }
    }
}


/**
 * While build 1 is running, build 2 fires. It has milestone 1 and milestone 2.
 * It passes milestone 1, which causes build 1 to abort.
 */
void killOldBuild() {
    def buildNumber = env.BUILD_NUMBER as int

    if (buildNumber > 1) {
        milestone(buildNumber - 1)
    }

    milestone(buildNumber)
}
