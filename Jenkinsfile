pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building.. (Branch is: ${env.BRANCH_NAME})"
            }
        }
        stage('Test') {
            steps {
                echo "Testing.."
            }
        }
        stage('Deploy to dev') {
		    when {
				branch 'develop'
			}
            steps {
                echo 'Deploying to Dev....'
            }
        }
		stage('Deploy to prod') {
		    when {
				branch 'master'
			}
            steps {
                echo 'Deploying to Prod....'
            }
        }
    }
}
