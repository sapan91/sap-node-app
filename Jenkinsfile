pipeline {
	agent any
		stages{
		stage ("build") {
		steps {
			sh 'sudo apt-get install npm'
			sh 'npm install'
			sh 'nmp run build'
			echo "Building complete"

}
}
}
		
}
