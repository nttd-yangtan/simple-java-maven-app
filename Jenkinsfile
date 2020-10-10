pipeline {
    agent none
    stages {
        stage('Build') {
            agent {
                docker {
                    image 'maven:3-alpine' 
                    args '-v /root/.m2:/root/.m2' 
                }
            }
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('Deploy') {
            agent {
                docker {
                    image 'python:v1' 
                    args '-v /opt/jenkins-data01/workspace/simple-java-maven-app/target:/root/target' 
                }
            }
            steps {
                sh 'aws lambda update-function-code --function-name  jenkins-java-test --zip-file fileb:///root/target/java-basic-1.0-SNAPSHOT.jar --region ap-northeast-1' 
            }
        }
    }
}
