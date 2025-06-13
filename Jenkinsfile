// node {
//     def app

//     stage('Clone repository') {
//         checkout scm
//     }

//     stage('Build image') {
//        app = docker.build("devops/jenkins-flask")
//     }

//     stage('Test image') {
//         app.inside {
//             sh 'echo "Tests passed"'
//         }
//     }

//     stage('Push image') {
//         docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
//             app.push("${env.BUILD_NUMBER}")
//         }
//     }
    
//     stage('Trigger ManifestUpdate') {
//         echo "triggering updatemanifestjob"
//         build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
//     }
// }
node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
        app = docker.build("mohamedalirezgui/jenkins-flask")
    }

    stage('Test image') {
        app.inside {
            sh 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
        }
    }

    stage('Trigger ManifestUpdate') {
        echo "triggering updatemanifestjob"
        build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
    }
}
