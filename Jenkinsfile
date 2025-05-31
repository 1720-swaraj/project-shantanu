pipeline{
	agent{
		label 'built-in'
	}

	stages{
		stage('stage-1'){
			dir('/mnt/'){
			sh 'echo "clonning git project"'
			sh 'git clone https://github.com/1720-swaraj/project-shantanu.git'
			}
		}
		stage('stage-2'){
			sh 'echo "maven clean install"'
			sh 'sudo mvn clean install'
		}
	}
}