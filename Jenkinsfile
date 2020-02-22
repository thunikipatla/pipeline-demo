pipeline{
agent any
  stages{
    stage('SCM'){
      steps{
        git 'https://github.com/thunikipatla/pipeline-demo.git'
      }
    }
    stage('Build'){
      steps{
        sh ''' mvn package '''
      }
    }
    stage('Archive-Artifacts'){
      steps{
        archiveArtifacts 'target/demo_*'
      }
    }
  }
}
