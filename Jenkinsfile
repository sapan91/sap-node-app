pipeline
{
agent any

	environment {
		EC2_HOST = '13.127.181.47'
		SSH_CREDENTIAL_ID = 'ubuntukey.pem'
		REMOTE_USER = 'ubuntu'
		REMOTE_PATH = '/home/ubuntu/app'
		WEB_ROOT = '/var/www/html'
		//DEPLOY_DIR = '/var/www/html'
		SERVICE_NAME = 'nginx'
		}
	
	stages {
		stage ("Build") {
		steps {
		echo 'Installing dependencies...'
		sh 'npm install'
		echo 'Building the application'
		sh 'npm run build'
		echo 'Build complete'
}
}

		stage('Deploy') {

			steps {
				echo 'Deploying to EC2 as '+ env.EC2_HOST
				sshagent (credentials: [env.SSH_CREDENTIAL_ID]) {
					sh """
     				echo "Creating remote directory..."
	 	ssh -o StrictHostKeyChecking=no ${REMOTE_USER}@${EC2_HOST} 'mkdir -p ${REMOTE_PATH}'
   		echo "Copying build to remote EC2 ..."
     		scp -o StrictHostKeyChecking=no -r dist/* ${REMOTE_USER}@${EC2_HOST}/
       		echo "Moving files to web root and restarting nginx"
	 	ssh ${REMOTE_USER}@${EC2_HOST} '
   		sudo rm -rgf ${WEB_ROOT}/*
     		sudo cp -r ${REMOTE_PATH}/* ${WEB_ROOT}/
       		sudo systemctl restart nginx
		'
  	"""
  		
	/*	
steps {
	echo 'Deploying build to local web server'

	sh '''
	echo "Copying build to $DEPLY_DIR"
	sudo rm -rf ${DEPLOY_DIR}/*
	sudo cp -r dist/* ${DEPLOY_DIR}/
	echo "Restarting $SERVICE_NAME"
	sudo systemctl restart ${SERVICE_NAME}
	'''
*/
	echo 'Deployment Completed'
	}
}
}
}
