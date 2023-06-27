node {
    stage('Build') {
        docker.image('node:lts-buster-slim').inside {
            if (changedFiles().contains('package.json')) {
                echo 'File changed, execute npm install'
                sh 'npm install'
            }
        }
    }
    stage('Test') {
        docker.image('node:lts-buster-slim').inside {
            sh './jenkins/scripts/test.sh'
        }
    }
    stage('Deploy') {
        docker.image('node:lts-buster-slim').inside('-p 3000:3000') {
            sh './jenkins/scripts/deliver.sh'
            input message: 'Finished using the web site? (Click "Proceed" to continue)'
            sh './jenkins/scripts/kill.sh'
        }
    }
}
