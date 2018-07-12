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
    stage('Deploy') {
      options {
        timeout(time: 10, unit: 'SECONDS')
      }
      input {
        message 'Should we continue?'
        ok "Deploy"
        parameters {
          choice(name: 'APP_VERSION', choices: "v1.1\nv1.2\nv1.3", description: 'what to deploy?')
        }
      }
      steps {
        echo "continuing with deployment ${APP_VERSION}"
      }
      
      post {
        aborted {
          echo 'Why didn\'t you push my button?'
        }
        success {
          echo 'build success!'
        }
        failure {
          echo 'failure'
        }
        unstable {
          echo 'unstable'
        }
        changed {
          echo 'changed'
        }
        regression {
          echo 'regression'
        }
        fixed {
          echo 'fixed'
        }
        cleanup {
          echo 'cleanup'
        }
        
      }
    }
  }
  environment {
    MY_NAME = 'Beaver'
    TEST_USER = credentials('test-user')
  }
  parameters {
    string(name: 'Name', defaultValue: 'whoever you are', description: 'who should I say hi to?')
  }
}
