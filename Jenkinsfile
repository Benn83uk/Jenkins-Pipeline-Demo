pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo "Building.. (Branch is: ${env.BRANCH_NAME})"
            }
        }
        stage('Unit Test') {
            steps {
                echo "Running Unit Tests.."
            }
        }
        stage('Deploy to dev') {
			environment {
				DEPLOY_TO="development_server"
			}
            steps {
                echo "Deploying to (${env.DEPLOY_TO})...."
            }
        }
		stage('Integration Test') {
            steps {
                echo "Running Integration Tests.."
            }
        }
        stage('Deploy to UAT') {
		    when {
				branch 'master'
			}
			environment {
				DEPLOY_TO="uat_server"
			}
            steps {
				sh "git tag -a uat_build_${env.BUILD_NUMBER} -m \"Tagging prior to deployment to UAT\""
				sh "git push --tags"
                echo "Deploying to (${env.DEPLOY_TO})...."
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
				input message: "Approve build for deployment to Production?"
				sh "git tag -a prod_build_${env.BUILD_NUMBER} -m \"Tagging prior to deployment to Production\""
				sh "git push --tags"
                echo "Deploying to (${env.DEPLOY_TO})...."
            }
        }
    }
}
