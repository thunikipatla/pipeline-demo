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
    stage('Sonar-Stage'){
      steps{
        withSonarQubeEnv('sonar'){
            sh 'mvn clean package sonar:sonar'
        }
  }
 }
  stage('Quality-gate'){
      steps{
        sleep(60)
        script {
        qg=waitForQualityGate('sonarQuality')
        if (qg.status == 'OK'){
         echo "Quality gate passed"
        }
        else {
            error "The pipeline fialed due to my quality gate check"
        }
        }
         }
  }
  stage('upload-artifacts'){
      steps {
        nexusArtifactUploader artifacts: [[artifactId: 'dev', classifier: '', file: "./target/demo_artifact-1.1.jar", type: 'jar']], credentialsId: 'nexus', groupId: 'dev_group', nexusUrl: '192.168.34.11:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'RepoR', version: '1.1'
      }
  }
}
}
