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
		stage('Approval') {
			stepd {
				input message: "Approve build?" submitter: "admin_group"
			}
		}
        stage('Deploy to dev') {
		    when {
				branch 'develop'
			}
			environment {
				DEPLOY_TO="development_server"
			}
            steps {
                echo "Deploying to Dev (${env.DEPLOY_TO})...."
            }
        }
		stage('Deploy to prod') {
		    when {
				branch 'master'
			}
			environment {
				DEPLOY_TO="production_server"
			}
            steps {
                echo "Deploying to Prod (${env.DEPLOY_TO})...."
            }
        }
    }
}
