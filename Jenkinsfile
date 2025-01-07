pipeline {
    agent any
    tools {
        maven 'maven' 
        nodejs 'nodejs'
    }
    stages {
        stage("Clean up") {
            steps {
                deleteDir() 
            }
        }
        stage("Clone repos") {
            steps {
                sh 'git clone https://github.com/ghadaabassi/FullStackPipline.git'
            }
        }
        stage("Generate backend image") {
            steps {
                dir("FullStackPipline/springboot/app") { 
                    sh "mvn clean install"
                    sh "docker build -t backend ." 
                }
            }
        }
        stage("Generate Angular image") {
            steps {
                dir("FullStackPipline/angular-app") {
                    sh "npm install -g @angular/cli"
                    sh "npm install" 
                    sh "ng build --configuration production"
                    sh "docker build -t frontend ." 
                }
            }
        }
        stage("Run docker compose") {
            steps {
                dir("FullStackPipline") { 
                    sh "docker compose up -d"
                }
            }
        }

        stage("SonarQube Analysis") {
            steps {
                withSonarQubeEnv("sonar-server") { 
                     dir("FullStackPipline/springboot/app") { 
                    sh "mvn sonar:sonar"
                }
                }
            }
        }

        
    }
}
