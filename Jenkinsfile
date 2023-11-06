pipeline {
    agent any
     tools{
        nodejs 'frant'
    }
    
    environment {
    DOCKERHUB_CREDENTIALS = credentials('dockerhub')
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

         
        
        stage('Send Email Notification') {
            steps {
                dir('Back') {
                    script {
                        try {
                            sh 'mvn clean install'
                        } catch (Exception e) {
                            currentBuild.result = 'FAILURE'
                            error("Build failed: ${e.message}")
                        }
                    }
                }
            }

            post {
                success {
                    script {
                        def subject = "Test and Build Check"
                        def body = "BUILD GOOD"
                        def to = 't9876924@gmail.com'

                        mail(
                            subject: subject,
                            body: body,
                            to: to,
                        )
                    }
                }
                failure {
                    script {
                        def subject = "Build Failure - ${currentBuild.fullDisplayName}"
                        def body = "The build has failed "
                        def to = 't9876924@gmail.com'

                        mail(
                            subject: subject,
                            body: body,
                            to: to,
                        )
                    }
                }
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }
        stage('UNIT TESTES') {
            steps {
                dir('Back') {
                    script {
                        sh 'mvn clean install' 
                    }
                }
            }
        }

        stage('SONARQUBE') {
            steps {
                dir('Back') {
                sh 'mvn sonar:sonar -Dsonar.host.url=http://localhost:9000 -Dsonar.login=admin -Dsonar.password=ghazi123'
            }
            }
        }
        stage('NEXUS') {
            steps {
                dir('Back') {
                sh 'mvn clean deploy -DskipTests'
            }
            }
        }
        
        stage('BBUILD FRONT') {
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
        stage('LOGIN DOCKER') {
        steps {
        script {
            sh 'echo ghazi1234 | docker login -u ghazi11 --password-stdin'
                }
            }
        }      
        
        

        stage('CREATE DOCKER IMAGE BACK') {
            steps {
                dir('Back') {
                    script {
                        sh 'docker build -t ghazi11/back1 .'
                        sh 'docker push ghazi11/back1'
                    }
                }
            }
        }
        stage('CREATE DOCKER IMAGE FRONT') {
            steps {
                dir('Frant') {
                    script {
                        sh 'docker build -t ghazi11/frant .'
                        sh 'docker push ghazi11/frant'
                        
                    }
                }
            }
        }
        
        stage('DEPLOY APP') {
            steps {
                
                script {
                    sh 'docker-compose -f docker-compose.yml up -d' 
                    sh 'docker-compose -f docker-compose.yml start'                       
                }
                
            }
        }
}
}






