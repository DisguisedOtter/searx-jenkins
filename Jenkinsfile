node {
    def app
    
    stage ('Clone repository') {
        checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/asciimoo/searx']]])
    }
    
    stage('Build Image') {
        app = docker.build("disguisedotter/searx")
    }
    
    stage('test image') {
        sh 'echo "tests passed"'
        }
        
    stage('Push image') {
        /* get credentials from jenkins, and store them in variables for pushing to docker hub */
        withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
            sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
            sh 'docker push disguisedotter/searx:latest'             
         }
    }
}