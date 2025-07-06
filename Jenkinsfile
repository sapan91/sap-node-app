pipeline {
	agent any

	environment {
		EC2_USER = 'ubuntu'
		EC2_HOST = '13.233.227.213'
		SSH_CREDENTIAL_ID = 'ec2-ssh-key'
	}
		stages{
		stage ("build") {
		steps {
			
			sh 'npm install'
			sh 'npm run build'
			echo "Building complete"
		}
		
		stage ("Deploy")	
		steps { 
		echo "Strat Deployment on EC2"
		sshagent(['ec2-ssh-key']) {
			sh '''
				echo "Copying build artifacts to EC2"
				scp -o strictHostKeyChecking=no -r dist/ ubuntu@13.233.227.213:/var/www/html
				echo "Restarting web server on EC2"
				ssh -o strictHostKeyChecking=no ubuntu@13.233.227.213 'sudo systemctl restart nginx'
			'''
		}
			echo "Deployment Completed"
		}

}
}
}
		
