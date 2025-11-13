pipeline{
    agent any

    tools{
        jdk 'java-17'
        maven 'maven'
    }

    environment{
        IMAGE_NAME='kjtejasvi/itkannadigaru-blogpost:${GIT_COMMIT}'
    }
    stages{
        stage('Git-checkout'){
            steps{
                  git url: 'https://github.com/KjTejasvi/ITKannadigaru-Java-based-app.git', branch:'prod'
            }
        }
        stage('compile'){
            steps{
                sh'''
                    mvn compile
                '''
            }
        }
        stage('package'){
            steps{
                sh'''
                    mvn package
                '''
            }
        }
        stage('Docker-build'){
            steps{
                sh'''
                  docker build -t ${IMAGE_NAME} .
                '''
            }
        }
        stage('Docker-Testing'){
            steps{
                sh'''
                  docker run -it -d --name itkannadigaru-blogpost -p 9000:8080 ${IMAGE_NAME}
                '''
            }
        }
    }
}
