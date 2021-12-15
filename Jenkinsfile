pipeline {
  environment {
    registry = "998966/spring-petclinic-hub"
    registryCredential = 'docker-hub'
    dockerImage = ''
  }
  agent pipeline {
  environment {
    registry = "998966/spring-petclinic-hub"
    registryCredential = 'docker-hub'
    dockerImage = ''
  }
  agent { label 'demo' }
  tools {
    maven 'Maven 3.3.9'
    jdk 'jdk8'
  } 
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/998966/spring-petclinic-jenkins-pipeline.git'
      }
    }
    stage('Compile') {
       steps {
         sh 'mvn compile' //only compilation of the code
       }
    }
    stage('Test') {
      steps {
        sh '''
        mvn clean install
        ls
        pwd
        ''' 
        //if the code is compiled, we test and package it in its distributable format; run IT and store in local repository
      }
    }
    stage('Building Image') {
      steps{
        script {
          dockerImage = docker.build registry + ":latest"
        }
      }
    }
    stage('Deploy Image') {
      steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:latest"
      }
    }
  }
}
  tools {
    maven 'Maven 3.3.9'
    jdk 'jdk8'
  } 
  stages {
    stage('Cloning Git') {
      steps {
        git 'https://github.com/998966/spring-petclinic-jenkins-pipeline.git'
      }
    }
    stage('Compile') {
       steps {
         sh 'mvn compile' //only compilation of the code
       }
    }
    stage('Test') {
      steps {
        sh '''
        mvn clean install
        ls
        pwd
        ''' 
        //if the code is compiled, we test and package it in its distributable format; run IT and store in local repository
      }
    }
    stage('Building Image') {
      steps{
        script {
          dockerImage = docker.build registry + ":latest"
        }
      }
    }
    stage('Deploy Image') {
      steps{
         script {
            docker.withRegistry( '', registryCredential ) {
            dockerImage.push()
          }
        }
      }
    }
    stage('Remove Unused docker image') {
      steps{
        sh "docker rmi $registry:latest"
      }
    }
  }
}
