pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        stage('Build Docker Image') {
            when {
                branch 'master'
            }
            steps {
                script {
                    app = docker.build("surajkeshri/train-schedule")
                    app.inside {
                        sh 'sleep 2; echo $(curl localhost:8080)'
                    }
                }
            }
        }
    }
}