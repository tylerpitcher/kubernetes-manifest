node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Update GIT') {
      script {
          catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
              withCredentials([usernamePassword(credentialsId: 'github-username-token', usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD')]) {
                  sh "cat deployment.yaml"
                  sh "sed -i 's+tylerpitcher/test.*+tylerpitcher/test:${DOCKERTAG}+g' deployment.yaml"
                  sh "echo ----------------------------------------------"
                  sh "cat deployment.yaml"
                  // sh "git config --global user.name ${USERNAME}"
                  // sh "git commit -am 'Updated version number'"
                  sh "git add ."
                  sh "git commit -m 'Change manifest: ${env.BUILD_NUMBER}'"
                  sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${USERNAME}/kubernetes-manifest.git"
      }
    }
  }
}
}
