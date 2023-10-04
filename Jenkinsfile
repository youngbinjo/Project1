// node {
//     def app
//     stage('Clone repository') {
//         checkout scm
//     }
//     stage('Update GIT') {
//             script {
//                 catchError(buildResult: 'SUCCESS', stageResult: 'FAILURE') {
//                     withCredentials([usernamePassword(credentialsId: 'github', passwordVariable: 'GIT_PASSWORD', usernameVariable: 'GIT_USERNAME')]) {
//                         //def encodedPassword = URLEncoder.encode("$GIT_PASSWORD",'UTF-8')
//                         sh "git config user.email youngbin9806@gmail.com"
//                         sh "git config user.name youngbinjo"
//                         //sh "git switch master"
//                         sh "cat deployment.yaml"
//                         sh "sed -i 's+youngbinjo/test.*+youngbinjo/test:${DOCKERTAG}+g' deployment.yaml"
//                         sh "cat deployment.yaml"
//                         sh "git add ."
//                         sh "git commit -m 'Done by Jenkins Job changemanifest: ${env.BUILD_NUMBER}'"
//                         sh "git push https://${GIT_USERNAME}:${GIT_PASSWORD}@github.com/${GIT_USERNAME}/Project1.git HEAD:main"
//       }
//     }
//   }
// }
// }

pipeline {
    agent any

    stages {
        stage('Clone repository') {
            steps {
                // GitHub 저장소에서 코드를 가져옵니다.
                checkout scm
            }
        }

        stage('Apply Deployment') {
            steps {
                // Kubernetes에 deployment.yaml 파일을 적용합니다.
                script {
                    sh 'kubectl apply -f deployment.yaml'
                }
            }
        }
    }
}
