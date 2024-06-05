pipeline {
        agent any
        stages {

        stage("Source") {
          agent any
          steps {
              git branch: 'master', url: 'https://github.com/BINPIPE/java-springboot-sonarqube.git'
          }
        }

        
          stage("Build") {
            agent any
            steps {
                bat 'mvn clean package'
            }
          }

          stage('SonarQube analysis') {
	    steps {
	        withSonarQubeEnv(installationName: 'sq1') {
	            bat "mvn clean verify sonar:sonar -Dsonar.projectKey=sonarcodecoverage -Dsonar.projectName='sonarcodecoverage'"
		}
            }
        }

          stage('Approve Deployment') {
              agent any
              input{
                   message "Do you want to proceed for deployment?"
                      }
              steps {
                  //Add deploy steps & Alerts below
                  bat 'echo "Deploying into Server"' 

                }
          } 
          
        } // stage
        
        
        
      }
