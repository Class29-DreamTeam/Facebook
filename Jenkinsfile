	pipeline{
	  agent any 
	  tools {
	    maven "maven3.8.6"
	  }  
	  stages {
	    stage('1CloneCode'){
	      steps{
	        sh "echo 'cloning the latest application version' "
	        git credentialsId: 'Githubcredential', url: 'https://github.com/Class29-DreamTeam/Facebook.git'
	      }
	    }
	    stage('2Test&Build'){
	      steps{
	        sh "echo 'running JUnit-test-cases' "
	        sh "echo 'testing must passed to create artifacts ' "
	        sh "mvn clean package"
	      }
	    }
	    stage('3CodeQuality'){
	      steps{
	        sh "echo 'Perfoming CodeQualityAnalysis' "
	        sh "mvn sonar:sonar"
	      }
	    } 
	    stage('4uploadNexus'){
	      steps{
	        sh "mvn deploy"
	      }
	    }  
	    stage('5deploy2prod'){
	      steps{
	        deploy adapters: [tomcat9(credentialsId: '27538aa4-cb0f-483b-b7b0-c230598a4625', path: '', url: 'http://52.207.4.208:8080/')], contextPath: null, war: 'target/*war'
	    }     
	  }
	}
	}

