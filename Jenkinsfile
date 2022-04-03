pipeline {
    agent{
        label "test"
    }

    stages {
        stage('Run Script') {
            steps {
                dir("Temp"){
                git branch: "master",
                    url: "https://github.com/dockersamples/node-bulletin-board"
                powershell """
                cd bulletin-board-app
                ../.././change.sh
                """
                }
            }
        }
        stage('Docker: Build Image') {
            steps {
                script{
                    withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                        powershell """
                        cd Temp\\bulletin-board-app\\
                        docker build -t $USERNAME/bulletin-app:1.0.0 .
                        """
                    }
                }
            }
        }
        stage('Docker: Push Image') {
            steps {
            withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    powershell """
                    docker push $USERNAME/bulletin-app:1.0.0
                    """
                }
            }
        }
        stage('Helm: Deploy'){
            steps {
                powershell """
                helm upgrade --install bulletin-app . -n demo
                """
            }
        }
    }
}
