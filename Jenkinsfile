pipeline {
    agent any

    stages {
        stage('Run Script') {
            steps {
                dir("Temp"){
                git branch: "master",
                    url: "https://github.com/dockersamples/node-bulletin-board"
                sh """
                ls -R
                cd bulletin-board-app
                chmod +x ../../change.sh
                ../.././change.sh
                """
                }
            }
        }
        stage('Build Image') {
            steps {
                script{
                    def dockerHome = tool 'docker'
                    env.PATH = "${dockerHome}/bin:${env.PATH}"
                    sh ""
                    withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        sh """
                        systemctl start docker
                        cd Temp/bulletin-board-app/
                        docker build -t \$USERNAME/bulletin-app:1.0.0 .
                        docker login -u \$USERNAME -p \$PASSWORD
                        """
                    }
                }
            }
        }
    }
}
