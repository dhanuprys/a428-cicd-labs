node {
    stage('Build') {
        docker.image('node:lts-buster-slim').inside {
            sh 'npm install'
        }
    }
    stage('Test') {
        docker.image('node:lts-buster-slim').inside {
            sh './jenkins/scripts/test.sh'
        }
    }
    stage('Deploy') {
        docker.image('node:lts-buster-slim').withRun('-p 3000:3000') {
            sh './jenkins/scripts/deliver.sh'
            input message: 'Finished using the web site? (Click "Proceed" to continue)'
            sh './jenkins/scripts/kill.sh'
        }
    }
}
