pipeline {
    agent any
	
	environment {
		GITHUB_ACCESS_TOKEN = credentials('benn83-github-public-token')
		REPO_URL = 'github.com/Benn83uk/Jenkins-Pipeline-Demo.git'
		NOTIFY_FOR_APPROVAL = 'ben.noble@paconsulting.com'
	}

    stages {
        stage('Build') {
            steps {
                echo "Building.. (Branch is: ${env.BRANCH_NAME})"
				//TODO: add command for Building (eg, 'mvn package')
            }
        }
        stage('Unit Test') {
            steps {
                echo "Running Unit Tests.."
				//TODO: add command for Running Unit Test (eg, 'mvn test').
            }
        }
        stage('Deploy to dev') {
			environment {
				DEPLOY_TO="development_server"
			}
            steps {
                echo "Deploying to (${env.DEPLOY_TO})...."
				//TODO: add commands for Deploying to your development environment
            }
        }
		stage('Integration Test') {
            steps {
                echo "Running Integration Tests.."
				//TODO: add command for running Integration tests
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
				sh("git push https://${env.GITHUB_ACCESS_TOKEN}@${env.REPO_URL} --tags")
                echo "Deploying to (${env.DEPLOY_TO})...."
				//TODO: add commands for Deploying to your UAT environment
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
				mail subject: "Approve Build", body: "Approve build with link", from: "jenkins@paconsulting.com", to:"${NOTIFY_FOR_APPROVAL}"
				input message: "Approve build for deployment to Production?"
				
				sh "git tag -a prod_build_${env.BUILD_NUMBER} -m \"Tagging prior to deployment to Production\""
				sh("git push https://${env.GITHUB_ACCESS_TOKEN}@${env.REPO_URL} --tags")
                echo "Deploying to (${env.DEPLOY_TO})...."
				//TODO: add commands for Deploying to your Production environment
            }
        }
    }
} 