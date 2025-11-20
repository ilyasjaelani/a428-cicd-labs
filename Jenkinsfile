node {
    // Checkout source code dari repo (branch sudah diatur di job)
    checkout scm

    // Jalankan build & test di dalam container Docker node:16-buster-slim
    docker.image('node:16-buster-slim').inside('-p 3000:3000') {

        stage('Build') {
            sh 'npm install'
        }

        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
    }
}
