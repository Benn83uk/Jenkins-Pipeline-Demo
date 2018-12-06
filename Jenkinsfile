pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
				sh 'printenv'
                echo "Building.. (Branch is: ${env.BRANCH_NAME}"
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
