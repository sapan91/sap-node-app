pipeline {
	agent any
		stages{
		stage ("build") {
		steps {
			
			sh 'npm install'
			sh 'npm run build'
			echo "Building complete"
		}
		stage ("Deploy"){
		steps { 
		echo "Strat Deployment on EC2"
		sh "scp -r -o strictcheckingOfKey=No" ./dist/* /home/ubuntu/node-app/"
		sh "npm start"
		echo "Deployment Completed"
		}
	}

}
}
}
		
