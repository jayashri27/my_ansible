pipeline{
    agent any
    stages{
            stage('build'){
            steps{
                cleanWs()
               }
            }
            stage('SCM checkout'){
            steps{
               git branch: 'main' , url: 'https://github.com/jayashri27/my_ansible.git'
            }
        }
            stage('execute ansible'){
            steps{
                ansiblePlaybook credentialsId: 'private-key', disableHostKeyChecking: true, installation: 'ansible', inventory: 'dev.inv', playbook: 'apache.yml' 
                
                
            }
        }
            stage('SonarQube Analysis') {
            steps {
                script{
                    def scannerHome = tool'SonarQube';
                    withSonarQubeEnv("SonarQube") 
                    {
                    sh "${tool("SonarQube")}/bin/sonar-scanner"
                    //sh "${scannerHome}/bin/sonar-scanner"
                     sonar-scanner
                     sonar.projectKey=ne
                     sonar.sources=/var/lib/jenkins/workspace/demo_jen
                     sonar.host.url="http://18.191.61.226:9000"
                     sonar.login=114ddca4651636956f3ce8390f39d9bb4635be4f
                    
                     
			    	}
			      }   
               }
            }
        }
    }
