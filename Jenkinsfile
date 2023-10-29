pipeline {
    agent any
     tools{
        nodejs 'frant'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Send Email Notification') {
            steps {
                script {
                    def contenuReadMe = readFile('README.md')
                    
                    def subject = 'New Project Commit - Mario'
                    def body = "A new commit has been made to the repository..\n\n${contenuReadMe}"
                    def to = 't9876924@gmail.com'
                    
                    mail(
                        subject: subject,
                        body: body,
                        to: to,
                    )
                }
            }
        }
        stage('Run Unit Tests') {
            steps {
                dir('Back') {
                    script {
                        sh 'mvn clean install' 
                    }
                }
            }
        }
        
        stage('Build Frontend') {
            steps {
                dir('Frant') {
                    script {
                        
                        
                        sh 'npm install -g @angular/cli'
                        sh  'npm install' 
                        sh 'ng build'      
                    }
                }
            }
        }
    }
}