pipeline {
    agent any

    stages {
        stage('Run Script') {
            steps {
                git branch: "master",
                    url: "https://github.com/dockersamples/node-bulletin-board"
                sh """
                cd bulletin-board-app
                chmod +x ../change.sh
                .././change.sh
                """
            }
        }
        stage('Build Image') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh """
                    cd bulletin-board-app
                    docker build -t \$USERNAME/bulletin-app:1.0.0 .
                    docker login -u \$USERNAME -p \$PASSWORD
                    """
                }
            }
        }
    }
}
