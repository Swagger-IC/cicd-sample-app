pipeline {
    agent any
    triggers {
        pollSCM 'H/5 * * * *'
    }
    stages {
        stage('Preparation') {
            steps {
                catchError(buildResult: 'SUCCESS') {
                    sh 'docker stop samplerunning || true' // Avoid failure if container isn't running
                    sh 'docker rm samplerunning || true'   // Avoid failure if container doesn't exist
                }
            }
        }
        stage('Build') {
            steps {
                build job: 'BuildSampleApp'
            }
        }
        stage('Results') {
            steps {
                build job: 'TestSampleApp'
            }
        }
    }
}
