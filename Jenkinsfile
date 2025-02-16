pipeline {
    agent any

    tools {
      maven 'maven'
    }
    
    environment{
        SCANNER_HOME = tool 'sonar-scanner'
    }
    stages {
        stage('Maven') {
            steps {
                script {
                    echo "Maven comlie and test for code coverage"
                        sh 'mvn clean package'
                }
            }
        }
        stage('SonarQube-analysis') { 
            steps {
                script {
                    echo "Sonar scanner"
                    withSonarQubeEnv('sonar-server') {
                    sh '''
                      ${SCANNER_HOME}/bin/sonar-scanner \
                      -Dsonar.projectKey=javakey \
                      -Dsonar.projectName=java-app \
                       -Dsonar.java.binaries=target/classes
                     '''
                    }     
                }
           }
        }
        stage('Build') {
            steps {
                script {
                    echo "docker build"
                        sh 'docker image prune -f'
                        sh 'docker build -t danushvithiyarth/java-app:latest .'
                }
            }
        }
        stage('Trivy-Check') {
            steps {
                script {
                    echo "trivy scan"
                        sh 'trivy image --format table -o report.html danushvithiyarth/java-app:latest'
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

      
