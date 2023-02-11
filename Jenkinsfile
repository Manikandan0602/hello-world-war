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
        stage("unit testing"){
            steps{
                
                sh 'mvn test'
            }
            post{
                success{
                     echo "junit testing is success,publishing report"
                     junit '**/surefire-reports/*.xml'
                
                }
                failure{
                    echo "junit testing is failed"

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
                        -Dsonar.host.url=http://34.220.100.149:9000 \
                        -Dsonar.login=sqp_4245d946c5ac6bbdf64df8c32431c278f5c75367"
    
                    }
                }
            }
        }
        stage("upload artifact"){
            steps{
               sh 'mvn -s settings.xml deploy'
            }
        }
    }
}