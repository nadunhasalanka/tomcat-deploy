pipeline {
    agent any
    
    tools {
        maven "Maven"
    }

    stages {
        stage('Clean workspace') {
            steps {
                cleanWs()
            }
        }
        stage('Git Clone') {
            steps {
                git branch: 'main', url: 'https://github.com/nadunhasalanka/tomcat-deploy.git'
            }
        }
        stage('Maven war file builder') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Docker  container/image deletion') {
            steps {
                script{
                    sh '''
                            # Stop the running container
                            if [ "$(docker ps -q -f name=maven-app)" ]; then
                                docker stop maven-app
                            fi

                            # Remove container if exists
                            if [ "$(docker ps -aq -f name=maven-app)" ]; then
                                docker rm maven-app
                            fi

                            # Remove image if exists
                            if docker images -q nadexplorer050/maven-app:latest > /dev/null; then
                                docker rmi nadexplorer050/maven-app:latest
                            fi
                    '''
                }
            }
        }

        stage('Docker Image - Push to docker hub') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker', toolname: 'docker'){
                    sh '''   docker build -t mavenec2 .
                            docker tag mavenec2 nadexplorer050/maven-app:latest
                            docker push nadexplorer050/maven-app:latest    '''
                    }
                }
            }
        }
        stage('Docker  container creation') {
            steps {
                sh 'docker run -d -p 9000:8080 --name maven-app -t nadexplorer050/maven-app:latest'
            }
        }
    }
}
