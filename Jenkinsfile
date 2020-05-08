pipeline {
  agent {
    docker {
      image 'node:12'
      args '--network host'
    }

  }
  stages {
    stage('Build') {
      steps {
        sh 'ls -la'
        sh 'ls -la'
        sh 'ls'
        sh 'ls'
        sh '''
npx create-react-app example-react'''
      }
    }

    stage('Test') {
      steps {
        sh '''cd ./example-react
npm test'''
      }
    }

    stage('Sonar') {
      steps {
        sh 'docker run -t -u 1000:1000 -u root:root --privileged -e SONAR_HOST_URL=http://sonarqube:9000 -w $(pwd) -v $(pwd):$(pwd):rw,z -v $(pwd)@tmp:$(pwd)@tmp:rw,z -v $(which docker):/usr/bin/docker --network host --entrypoint ./entrypoint.sh sonarsource/sonar-scanner-cli'
      }
    }

  }
  environment {
    CI = 'true'
  }
}