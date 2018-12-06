pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
				sh 'printenv'
                echo 'Building.. (Branch is: ' + $BRANCH_NAME + ')'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing.. (Branch is: ${BRANCH_NAME}'
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
            }
        }
    }
}
