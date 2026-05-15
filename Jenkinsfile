pipeline {

    agent any

    tools {
        maven 'Maven3'
    }

    stages {

        stage('Clone Repository') {

            steps {

                git branch: 'master',
                url: 'https://github.com/rchna1989-hash/Staragile-assignment.git'

            }
        }

        stage('Build Maven Project') {

            steps {

                sh 'mvn clean package'

            }
        }

    }

    post {

        success {

            echo 'Build Successful'

        }

        failure {

            echo 'Build Failed'

        }

    }
}