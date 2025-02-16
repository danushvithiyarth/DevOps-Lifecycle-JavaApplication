pipeline {
    agent any

    environment{
        SCANNER_HOME = tool 'sonar-scanner'
    }
    stages {
        stage('SonarQube-analysis') { 
            steps {
                script {
                    echo "Sonar scanner"
                    withSonarQubeEnv('sonar-server') {
                    sh '''
                      ${SCANNER_HOME}/bin/sonar-scanner \
                      -Dsonar.projectKey=nodekey \
                      -Dsonar.projectName=nodejs \
                      -Dsonar.java.binaries=target
                     '''
                    }     
                }
           }
        }
        stage('Build') {
            steps {
                script {
                    echo "docker build"
                        sh 'docker build -t danushvithiyarth/java-app:latest .'
                }
            }
        }
        stage('Trivy-Check') {
            steps {
                script {
                    echo "trivy scan"
                        sh 'trivy image --format table -o report.html .'
                }
            }
        }
        stage('DockerHub image push') {
            steps {
                script {
                    echo "Image push"
                        sh 'docker login -u "danushvithiyarth" -p "$Docker_pass" docker.io'
                        sh 'docker push danushvithiyarth/java-app:latest'
                }
            }
        }
    }
}

      
