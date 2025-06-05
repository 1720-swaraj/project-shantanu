pipeline{
    agent{
        label 'built-in'
    }
    tools{
        maven 'install-maven'
    }
    stages{
        stage('stage-1'){
            steps{
                cleanWs()
                sh 'echo "project clonning"'
                git url: 'https://github.com/1720-swaraj/project-shantanu.git', branch: 'master'
            }
        }
    }
}

/*
install java
install jenkins
inside /var/lib/ systemctl start jenkins & systemctl enable jenkins
login to jenkins
install git
install maven
inside /root/.bash_profile MAVEN_HOME
source .bash_profile
git clone repository
give jenkins file permission /mnt, $WORKSPACE
cd target && rm -rf target
inside workspace where pom.xml is present mvn clean install
checkout scm
stash 'source-code' format '*.war'
*/

