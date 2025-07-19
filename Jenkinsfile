pipeline
{
agent any

	environment {
		DEPLOY_DIR = '/var/www/html'
		SERVICE_NAME = 'ngix'
		}
	
	stages {
		stage ("Build")
		step{
		echo 'Installing dependencies...'
		sh 'npm install'
		echo 'Building the application'
		sh 'npm run build'
		echo 'Build complete'
}
}

		stage('Deploy') {
		
steps {
	echo 'Deploying build to local web server'

	sh '''
	echo "Copying build to $DEPLY_DIR"
	sudo rm -rf ${DEPLOY_DIR}
	sudo cp -r dist/* ${DEPLOY_DIR}
	echo "Restarting $SERVICE_NAME"
	sudo systemctl restart ${SERVICE_NAME}
	'''

	echo 'Deployment Completed'
	}
}
}
}
