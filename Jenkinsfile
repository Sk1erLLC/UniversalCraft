pipeline {
  agent any
  stages {
    stage('Initialize') {
      steps {
        sh '''
        ./gradlew clean
        ./gradlew preprocessResources
        '''
      }
    }

    stage('Build') {
      steps {
        sh "./gradlew publish -PBUILD_ID=${env.BUILD_ID} -Pbranch=${env.BRANCH_NAME} -PIS_CI=true --no-daemon"
      }
    }

    stage('Report') {
      steps {
        archiveArtifacts 'versions/1.8.9/build/libs/*.jar'
        archiveArtifacts 'versions/1.12.2/build/libs/*.jar'
        archiveArtifacts 'versions/1.15.2/build/libs/*.jar'
        archiveArtifacts 'versions/1.16.2/build/libs/*.jar'
        archiveArtifacts 'versions/1.16.2-fabric/build/libs/*.jar'
      }
    }
  }
}
