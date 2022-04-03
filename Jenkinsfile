pipeline {
    agent any

    stages {
        stage('Run Script') {
            steps {
                sh """
                chmod +x change.sh
                ./change.sh
                """
            }
        }
    }
}
