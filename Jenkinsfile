pipeline {
    agent any

stages {
    stage('Build') {
        agent { //here we select only docker build agents
            docker {
                image 'maven:latest' //container will start from this image
                args '-v /root/.m2:/root/.m2' //here you can map local maven repo, this let you to reuse local artifacts
                args '--network host'
            }
        }
        steps {
            sh 'mvn -B -DskipTests clean package' //this command will be executed inside maven container
        }
    }
    stage('Test') { //on this stage New container will be created, but current pipeline workspace will be remounted to it automatically
        agent {
            docker {
                image 'maven:latest'
                args '-v /root/.m2:/root/.m2'
                args '--network host'
          }
        }
        steps {
            sh 'mvn test'
        }
    }
}

}

