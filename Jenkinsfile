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
                    withDockerRegistry(credentialsId: 'docker', url: "") {
                        newBuild = docker.build("nourhankhalifa/bulletin-app:1.0.0", ".")
//                         newBuild.push()
                    }
                }
//                 withCredentials([usernamePassword(credentialsId: 'docker', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    
//                     sh """
//                     cd Temp/bulletin-board-app
//                     docker build -t \$USERNAME/bulletin-app:1.0.0 .
//                     docker login -u \$USERNAME -p \$PASSWORD
//                     """
//                 }
            }
        }
    }
}
