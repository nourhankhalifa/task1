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
        stage('Build Image') {
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
        stage('Push Image') {
            steps {
            withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    powershell """
                    docker push $USERNAME/bulletin-app:1.0.0
                    """
                }
            }
        }
    }
}
