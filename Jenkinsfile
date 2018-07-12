pipeline {
  agent {
    label 'jdk8'
  }
  stages {
    stage('Say Hello') {
      steps {
        echo "Hello ${params.Name}!"
        echo "${TEST_USER_USR}"
        echo "${TEST_USER_PSW}"
        sh 'java -version'
      }
    }
    stage('Testing') {
      failFast true
      parallel {
        stage("Java 8") {
          agent { label 'jdk8' }
          steps {
            sh 'java -version'
            sleep time: 10, unit: 'SECONDS'
          }
        }
        stage("Java 9") {
          agent { label 'jdk9' }
          steps {
            sh 'java -version'
            sleep time: 20, unit: 'SECONDS'
          }
        }
      }
    }
    
    stage('Checkpoint') {
      agent none
      steps {
        checkpoint 'Checkpoint'
      }
    }
    stage('Deploy') {
      steps {
        echo "continuing with deployment"
      }
      
      post {
        aborted {
          echo 'Why didn\'t you push my button?'
        }
      }    
    }
    stage('Get Kernel') {
      steps {
        script {
          try {
            KERNEL_VERSION = sh (script: "uname -r", returnStdout: true)
          } catch(err) {
            echo "CAUGHT ERROR: ${err}"
            throw err
          }
        }
      }
    }
    stage('Say Kernel') {
      steps {
        echo "${KERNEL_VERSION}"
      }
    }
  }
  environment {
    MY_NAME = 'Beaver'
    TEST_USER = credentials('test-user')
  }
}
