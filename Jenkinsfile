pipeline{
	agent{
		label 'built-in'
	}

	stages{
		stage('stage-1'){
			steps{
				dir('/mnt/new'){
				sh 'echo "this is our $WORKSPACE"'
				cleanWs()
				sh 'echo "clonning git project"'
				sh 'git clone https://github.com/1720-swaraj/project-shantanu.git'
			}
			}
			
		}
		stage('stage-2'){
			steps{
				sh 'echo "this is our $WORKSPACE"'
				sh 'echo "maven clean install"'
				sh 'sudo /var/lib/jenkins/workspace/jenkins-pipeline/mvn clean install'
			}
			
		}
	}
}