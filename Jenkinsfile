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
                  -Dsonar.host.url=http://65.0.179.34:9000 \\
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
                deploy adapters: [tomcat9(credentialsId: 'tomcat-id', path: '', url: 'http://13.201.74.48:8091')], contextPath: 'JAVA-APP', war: '**/*.war'
            }
        }
    }
}
