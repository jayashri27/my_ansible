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
                    
                    scannerHome = tool 'SonarQube';
                    withSonarQubeEnv('SonarQube') 
                    {
                    sh "${tool("SonarQube")}/bin/sonar-scanner"    
                    //sh "${scannerHome}/bin/sonar-scanner"
                    sonar.projectKey=sonar-check1
                    sonar.login=admin
                    sonar.password=admin
                    sonar.projectName=sonar-check1
                    sonar.sources=/var/lib/jenkins/workspace/sonar-check1
                    sonar.host.url='http://3.15.42.58:9000/'

                     
			    	}
			      }   
               }
            }
        }
    }
