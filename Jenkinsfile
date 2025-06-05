pipeline {
    agent {
        label 'built-in'
    }
    tools {
        maven 'install-maven'
    }
    stages {
        stage('stage-1-git-clone') {
            steps {
                cleanWs()
                sh 'echo "project clonning $WORKSPACE"'
                git url: 'https://github.com/1720-swaraj/project-shantanu.git', branch: 'master'
            }
        }
        stage('stage-2-maven-build') {
            steps {
                script {
                    if (fileExists('target')) {
                        sh 'rm -rf target'
                    }else {
                        echo "'target' folder does not exist — skipping deletion."
                    }

                    def warFiles = findFiles(glob: 'target/**/*.war')

                    if(warFiles.length == 0){
                        echo ".war file is not present"
                    }

                    def warFilePath = warFiles[0].path

                    stash name: "warFile" includes: "warFilePath"
                }
                sh '''
                mvn clean install
                cd target
                ls -lrta
                '''
            }
        }
        stage('stage-3-deploying-on-slave') {
            agent {
                label 'slave'
            }
            steps {
                dir('/mnt/server/apache-tomcat-10.1.41') {
                    
                    script {
                         if(fileExists('*.war')){
                            sh 'rm -rf *.war'
                         }else{
                            echo ".war is not existed"
                         }
                         unstash "warFile"
                         sh 'ls -lrta *.war'
                         sh 'mv *.war webapps'
                         sh '/bin/startup.sh'
                    }
                }
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
