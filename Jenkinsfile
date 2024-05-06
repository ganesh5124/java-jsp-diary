pipeline {
    agent any
    
    tools {
      jdk 'JAVA8'
    }
    stages {
        stage('CLONE SCM') {
            steps {
                echo 'CLONING FROM GIT REPO'
                git branch: 'master', url: 'https://github.com/ganesh5124/java-jsp-diary.git'
            }
        }
        stage('EXCUTE SHELL') {
            steps {
                echo 'CLONING FROM GIT REPO'
                sh 'mvn clean install'
            }
        }
        stage('EXCUTE SHELL FOR SONAR') {
            steps {
                echo 'CLONING FROM GIT REPO'
                echo "DISPLAYING SONAR"
                sh '''mvn sonar:sonar \\
                  -Dsonar.host.url=http://35.154.206.249:9000 \\
                  -Dsonar.login=9ae5023958a9a2eda6d0387949344df8da191944'''
            }
         
        }
        stage('EXCUTE SHELL FOR ARTIFACTORY') {
            steps {
                echo 'CLONING FROM GIT REPO'
                sh 'mvn clean deploy'
            }
        }
        

        
        stage('DEPLOY TO TOMCAT') {
            steps {
                echo 'DEPLOY TO TOMCAT'
                deploy adapters: [tomcat9(credentialsId: 'tomcat-id', path: '', url: 'http://3.110.92.81:8091')], contextPath: 'JAVA-APP', war: '**/*.war'
            }
        }
    }
    post {
        success {
            parallel {
                stage('Stage 1') {
                    steps {
                        echo 'Stage 1 executed'
                    }
                }
                stage('Stage 2') {
                    steps {
                        echo 'Stage 2 executed'
                    }
                }
            }
        }
    }
}
