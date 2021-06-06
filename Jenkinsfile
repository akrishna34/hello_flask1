pipeline {
    agent any
    options {
        timeout(time: 30, unit: 'SECONDS')   // timeout on whole pipeline job
    }

    stages {
        stage('Clone Repository') {
            options {
            timeout(time: 1, unit: 'MINUTES')   // timeout on whole pipeline job
        }
            steps {
                try {
                    checkout SCM
                    }
                catch(caughtError) {
                    deleteDir();
                    checkout SCM
                    }
            }
        }
        stage('Build') {
            steps {
                sh 'sudo docker build -t python_docker:v1 .'
            }
        }
        stage('Run Image') {
            steps {
                sh 'sudo docker run -it --name myfirstapp python_docker:v1'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying'
            }
        }
    }
    post {
        always {
            echo 'This will always run'
        }
        success {
            echo 'This will run only if successful'
        }
        failure {
            echo 'This will run only if failed'
        }
        unstable {
            echo 'This will run only if the run was marked as unstable'
        }
        changed {
            echo 'This will run only if the state of the Pipeline has changed'
            echo 'For example, if the Pipeline was previously failing but is now successful'
        }
    }
}