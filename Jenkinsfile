
pipeline {
    agent any
    tools {
     maven 'Maven 3.5.2'   
     jdk 'jdk1.8.0_151'
    }
    stages {
    stage('Build'){
      steps {
        bat 'mvn clean install'
      }
        post{
            success{
                junit 'target/surefire-reports/**/*.xml'
            }
        }  
    }
    
    stage('Test'){
      steps {
        bat "mvn test"
      }
      post{
            success{
                junit 'target/surefire-reports/**/*.xml'
            }
        } 
    }

    stage('Coverage Code'){
      steps {
        bat "mvn cobertura:cobertura -Dcobertura.report.format=xml"
      }
      post{
            success{
                cobertura coberturaReportFile: '**/target/site/cobertura/coverage.xml'
            }
        }

    }

    stage('JavaDoc Generation'){
      steps {
        bat "mvn javadoc:javadoc"
        bat "mvn site"
      }
    }

    stage("build & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('SonarCube') {
                bat 'mvn clean package sonar:sonar'
              }
            }
          }


   
    
    stage('Deploy'){
      steps {
        echo 'Deploying ..'
      }
    }
    
  }  
}
