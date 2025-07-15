pipeline{
	agent any

	environment{
		IMAGE_NAME = "orvencasido/ci-ci-node-app"
		DOCKERHUB_CREDENTIALS = credentials('dockerhub-creds')
	}

	stages{
		stage('Install Dependencies'){
			steps{
				sh 'npm install'
			}
		}
		stage('Test'){
			steps{
				sh 'npm test'
			}
		}
		stage('Build Docker Image'){
			steps{
				sh "docker build -t $IMAGE_NAME ."
			}
		}
		stage('Push to DockerHub'){
			steps{
				sh '''
					echo "$DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin"
					docker push $IMAGE_NAME
				'''
			}
		}
	}
}
