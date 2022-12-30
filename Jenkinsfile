pipeline {
  agent any
  
  stages {
    stage('Install Packages') {
      steps {
        sh 'npm install'
      }
    }
    stage('Create Build Artifacts') {
        steps {
            sh 'npm run build'
        }
    }

    stage('Production') {
        steps {
            withAWS(region:'us-east-1',credentials:'react-test') {
                s3Delete(bucket: 'testapp-react', path:'**/*')
                s3Upload(bucket: 'testapp-react', workingDir:'build', includePathPattern:'**/*');
            }
        }
    }
  }
}