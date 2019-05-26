pipeline {
  agent {
    node {
      label 'master'
    }
  }
  stages {
    stage('Checkout SCM') {
      steps {
        poll: false, url: 'git@hub.com:anup.dubey/nodejs-pipeline.git'
      }
    }
    stage('build docker images') {
      steps {
        sh '''docker build -t anuphnu/k8s-demo:$version .'''
      }
    }
    stage('login') {
      steps {
        sh '''docker login -u="anuphnu" -p="Notallow_123456"'''
      }
    }
    stage('push docker images') {
      steps {
        retry(2) {
            sh '''docker push anuphnu/k8s-demo:$version '''
        }
      }
    }
}
}
