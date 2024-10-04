pipeline {
    agent any

    stages {
        stage('fetching github code') {
            steps {
                // using echo to print message 
                echo 'we are now fetching github code in below'
                // using git to download git repo 
                git branch: 'main', url: 'https://github.com/bharath-b-1312/BB_DevSec_Flaskmysql.git'
                // using sh command to run some commands
                sh 'ls '
            }
        }
        // verify docker and trivy 
        stage('checking docker and compose status') {
            steps {
                echo 'checking docker status'
                sh 'docker version'
                echo 'checking docker compose status'
                sh 'docker-compose version'
                
            }
            
        }
        // using compsoe and curl 
        stage('compsoe for build and curl for app status test') {
            steps {
                echo 'running docker compose'
                sh 'docker-compose down'
                sh 'docker-compose up -d --build'
                sh 'docker-compose ps'
                sh 'curl -f http://localhost:3150'
            }
            
        }
        // using docker pipeline to build and push 
        stage('building image and pushing it') {
            steps {
                echo 'using docker pipeline plugin to build and push image'
                script {
                    def imageName = "bharath1312/flaskappday4"
                    def imageTag  = "appversion$BUILD_NUMBER"
                    def ashuCred = "27c08b75-0302-4ccb-a3d6-8c074d119785"
                    // building image 
                    docker.build(imageName + ":" + imageTag , " -f Dockerfile .")
                     pushing image to dockerhub
                    docker.withRegistry('https://registry.hub.docker.com',ashuCred){
                       docker.image(imageName + ":" + imageTag).push()
                  
                }
               
               
                

                }
            }
            
        }

    
    }
