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
  }
  environment {
    MY_NAME = 'Beaver'
    TEST_USER = credentials('test_user')
  }
  parameters {
    string(name: 'Name', defaultValue: 'whoever you are', description: 'who should I say hi to?')
  }
}