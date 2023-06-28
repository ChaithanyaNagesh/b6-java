pipeline{
    agent {
        label 'pwdslave'
    }
    tools {
        maven 'maven-3.6.3'
    }
    stages {

  stage('clean') {
    steps {
      sh 'mvn clean'
    }
  }
stage('build') {
    steps {
      sh 'mvn install'
    }
  }

  stage('test') {
    steps {
      sh 'mvn test'
    }

    post {
      always {
        archiveArtifacts artifacts: 'target/**.jar', followSymlinks: false
        junit 'target/surefire-reports/*.*xml'
      }
    }
  }

  stage('run') {
    steps {
      sh 'chmod 777 scripts/deliver.sh'
      sh './scripts/deliver.sh'
    }
  }

}

}
