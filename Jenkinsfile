pipeline {
  agent { label "jenkins-node" }    

  triggers {
    pollSCM('* * * * *')     
  }

  stages {
	  stage('Checkout') {
      steps {
        git branch: 'main', 
        url: 'https://github.com/Bart-90/CI-CD-home.git'   
      }
    }
    stage('Build') {
      steps {
        sh 'mvn clean package -DskipTest=true'
	}             
    }
    stage('Test') {
      steps {
        sh 'mvn test'               
      }
    }
    stage('Deploy') {
      steps {
        deploy adapters: [tomcat9(credentialsId: 'adminID', url: 'http://192.168.56.102:8080')], contextPath: null, war: 'target/hello-world.war'
      }
    }
  }
}
