pipeline {
    agent any

    stages {
        stage('Run Script') {
            steps {
                dir("temp"){
                    git branch: "master",
                        url: "https://github.com/dockersamples/node-bulletin-board"
                    sh """
                    cd bulletin-board-app
                    chmod +x ../../change.sh
                    ../.././change.sh
                    """
                }
            }
        }
    }
}
