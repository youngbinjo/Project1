node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Update GIT') {
            script {
                catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
                    withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
                        //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
                        sh "git config user.email youngbin9806@gmail.com"
                        sh "git config user.name youngbinjo"
                        //sh "git switch master"
                        sh "cat deployment.yaml"
                        sh "sed -i 's+youngbinjo/test.*+youngbinjo/test:${DOCKERTAG}+g' deployment.yaml"
                        sh "cat deployment.yaml"
                        sh "git add ."
                        sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
                        sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/Project1.git HEAD:main"
      }
    }
  }
}

    stage('Deployment Manifest File) {
        scripts {
            sh "curl -LO "curl -LO https://dl.k8s.io/release/v1.28.2/bin/linux/amd64/kubectl && chmod +x .kubectl && mv ./kubectl /usr/local/bin/kubectl"
            sh "kubectl apply -f deployment.yaml"
        }
    }
}
