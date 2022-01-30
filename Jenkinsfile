pipeline {
    agent any

    stages {
        stage('Pull') {
            steps {
                // Get HTML code from a GitHub repository
                git 'https://github.com/zubaer93/Basic-HTML-Website.git'
                sh 'ls -l'
            }
        }
        stage('deploy') {
            steps {
                script {
                    def remote = [:]
                    remote.name = "node-1"
                    remote.host = "<REMOTE-HOST-NAME>"
                    remote.allowAnyHosts = true
                    withCredentials([sshUserPrivateKey(credentialsId: 'deploy-server', keyFileVariable: 'identity', passphraseVariable: '', usernameVariable: 'userName')]) {
                        remote.user = userName
                        remote.identityFile = identity
                        
                        // start remote server
                        sshCommand remote: remote, command: 'sudo service nginx start'
                        
                        // copy repo to remote server
                        sshPut remote: remote, from: '.', into: '.'
                        
                        // move the html files to document root 
                        sshCommand remote: remote, command: 'sudo mv first-job/* /usr/share/nginx/html/; rm -rf first-job'
                    }
                }
            }
       }
        stage('Test') {
            steps {
                // Get HTML code from a GitHub repository
                sh 'curl http://<REMOTE-HOST-NAME>/'
            }
        }
    }
}
