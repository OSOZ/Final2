
pipeline {
    agent any
    tools {
     maven 'Maven 3.0.6'
     jdk 'jdk 1.8'
    }
    stages {
    stage('Build'){
      steps {
        sh 'mvn clean install'
      }
        post{
            success{
                junit 'target/surefire-reports/**/*.xml'
            }
        }  
    }
       
    
    stage('Test'){
      steps {
        sh "mvn test"
      }
      post{
            success{
                junit 'target/surefire-reports/**/*.xml'
            }
        } 
    }

    stage('Coverage Code'){
      steps {
        sh "mvn cobertura:cobertura -Dcobertura.report.format=xml"
      }
      post{
            success{
                cobertura coberturaReportFile: '**/target/site/cobertura/coverage.xml'
            }
        }

    }
	     stage('Performance Test'){
					steps{
						echo 'success'
					}
}
    
	     stage("build & SonarQube analysis") {
            agent any
            steps {
              //withSonarQubeEnv('SonarCube') {
                echo 'success'
          //    }
            }
          }

    stage('JavaDoc Generation'){
      steps {
        sh "mvn javadoc:javadoc"
        sh "mvn site"
      }
    }
	    
  stage('Packaging'){
			steps{
				sh 'mvn package'
		}
}


   
  stage('Archivage Nexus'){
		 steps {
        	echo 'Deploying ..'
      	}
}  
    stage('Deploy'){
      steps {
        echo 'Deploying ..'
      }
    }
    
  }  
}
