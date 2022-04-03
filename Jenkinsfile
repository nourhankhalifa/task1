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
                    withDockerRegistry(credentialsId: 'docker', url: "https://hub.docker.com/") {
                        sh "ls"
                        newBuild = docker.build("nourhankhalifa/bulletin-app:1.0.0", "bulletin-board-app/Dockerfile")
//                         newBuild.push()
                    }
                }
            }
        }
    }
}
