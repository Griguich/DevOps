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
         
        stage('Login Docker') {

            steps {
                sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u $DOCKERHUB_CREDENTIALS_USR --password-stdin'
            }
        
        }
        stage('Build & Push Docker Image (Backend)') {
            steps {
                dir('Back') {
                    script {
                        sh 'docker build -t ghazi11/back .'
                        sh 'docker push ghazi11/back'
                    }
                }
            }
        }

        stage('Build Docker Image (Frontend)') {
            steps {
                dir('Frant') {
                    script {
                        sh 'docker build -t ghazi11/frant .'
                        sh 'docker push ghazi11/frant'
                        
                    }
                }
            }
        }
    }
}





