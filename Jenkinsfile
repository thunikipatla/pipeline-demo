agent any 
  stages {
    stage('SCM'){
      steps {
        git 'https://github.com/thunikipatla/pipeline-demo.git'
      }
    }
    stage('Build') {
      steps {
        sh ''' echo "This stpe will build the mvn" '''
      }
    }
  }
}
