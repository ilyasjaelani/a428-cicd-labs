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

        stage('Manual Approval') {
            input message: 'Lanjutkan ke tahap Deploy?', ok: 'Proceed'
        }

        stage('Deploy') {
            sh 'chmod +x ./jenkins/scripts/deliver.sh ./jenkins/scripts/kill.sh'

            echo "Menjalankan React App..."
            sh './jenkins/scripts/deliver.sh'

            echo "Menjeda pipeline selama 1 menit agar React App dapat dicoba..."
            sh 'sleep 60'

            echo "Menghentikan React App..."
            sh './jenkins/scripts/kill.sh'
        } 
    }
}
