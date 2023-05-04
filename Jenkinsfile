pipeline {
    agent any
    stages{
        stage('download'){
            steps{
          checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url:
         'https://github.com/veeraboinaashok/simple-java-maven-app-master.git']])
            }
        }
        stage('build package'){
            steps{
                script{
                    sh 'mvn clean package'
                }
            }
        }
        stage('DeployIntoTomcat'){
            steps{
                script{
                    sh 'mv /var/lib/jenkins/workspace/java-jar-project/target/my-app-1.0-SNAPSHOT.jar  /var/lib/jenkins/workspace/java-jar-project/target/my-app-1.0-SNAPSHOT.war'
                    deploy adapters: [tomcat9(credentialsId: '32c279af-8017-4a49-b1ac-4058ff27bfcb', path: '', url: 'http://172.31.43.174:8080')], contextPath: 'qaenv', war: '**/*.war'
                }
            }
        }
    }
}
