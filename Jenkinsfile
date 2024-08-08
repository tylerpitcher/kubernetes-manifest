node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
      script {
          catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
              withCredentials([usernamePassword(credentialsId: 'github-username-password', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                  sh "cat deployment.yaml"
                  sh "sed -i 's+tylerpitcher/test.*+tylerpitcher/test:${DOCKERTAG}+g' deployment.yaml"
                  sh "cat deployment.yaml"
                  sh "git add ."
                  sh "git commit -m 'Change manifest: ${env.BUILD_NUMBER}'"
                  sh "git push https://${USERNAME}:${PASSWORD}@github.com/${USERNAME}/kubernetes-manifest.git HEAD:main"
      }
    }
  }
}
}
