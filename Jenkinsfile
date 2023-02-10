pipeline{
    agent any
    tools{
        maven 'maven-3'
    }
    stages{
        stage('build'){
            steps{
                script{
                    sh 'mvn clean install'
                }
            }
        }
        stage('sonar'){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonarqube') {
                    sh "${tool("sonarqube")}/bin/sonar-scanner \
                        -Dsonar.projectKey=hello-world-war \
                        -Dsonar.sources=. \
                        -Dsonar.java.binaries=target \
                        -Dsonar.host.url=http://34.218.238.209:9000 \
                        -Dsonar.login=sqp_4245d946c5ac6bbdf64df8c32431c278f5c75367"
    
                    }
                }
            }
        }

    }
}