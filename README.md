```groovy
pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Retrieving the source code from the specified directory path stored in the environment variable."
                echo "Compiling the code and producing necessary artifacts."
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo "Executing unit tests."
                echo "Conducting integration tests."
            }
        }

        stage('Code Evaluation') {
            steps {
                echo "Assessing code quality using an analysis tool."
            }
        }

        stage('Security Check') {
            steps {
                echo "Detecting vulnerabilities with a security scanning tool."
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo "Running integration tests on the staging environment."
            }
        }

        stage('Deployment to Production') {
            steps {
                echo "Deploying the code to the production environment."
            }
        }
    }

    post {
        success {
            emailext attachLog: true,
            compressLog: true,
            to: 'tanvirrahmantaiyeb@gmail.com',
            body: "Log available at $JENKINS_HOME/jobs/$JOB_NAME/builds/lastSuccessfulBuild/log",
            subject: "Production Deployment Success - Jenkins"
        }
        failure {  
            emailext attachLog: true,
            compressLog: true,
            to: 'tanvirrahmantaiyeb@gmail.com',
            body: "Log available at $JENKINS_HOME/jobs/$JOB_NAME/builds/lastSuccessfulBuild/log",
            subject: "Production Deployment Failure - Jenkins"
        }
    }
}
```

