pipeline {
  agent any
  stages {
    stage('clone') {
      steps {
        git(url: 'https://github.com/flyd0g/flask-hello-world.git', branch: 'containerized')
      }
    }

    stage('build') {
      steps {
        sh 'docker build -t adamhome/secondtest:latest .'
      }
    }

    stage('push') {
      steps {
        sh '''withCredentials([usernamePassword(credentialsId: \'dockerhub\', passwordVariable: \'dockerpassword\', usernameVariable: \'dockerusername\')]) {
    sh \'\'\'docker login -u ${dockerusername}-p ${dockerpassword}
docker push adamhome/secondtest:latest
\'\'\'
}'''
        }
      }

    }
  }