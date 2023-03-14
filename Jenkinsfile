pipeline {
    agent any
    tools{
        maven 'maven'
    }
    stages {
        stage('Code Checkoutcfrom github Repo') {
            steps {
              checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: '9df3f9ab-cfff-47aa-81c7-03728fd49152', url: 'https://github.com/Opas95/Jenkins-ci-cd-project.git']])
            }
        }
    stage ('Build with Maven') {
            steps {
                  sh 'mvn clean install -f pom.xml'
            }
        }
        stage('Mvn Test'){
            steps{
                sh '/usr/share/maven/bin/mvn test'
            }
        }    
        stage('Junit Test'){   
            steps{
                always {
                    junit '/var/lib/jenkins/workspace/JavaWebcalculator/target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deploy to tomcat'){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'tomcat_deployer', path: '', url: 'http://35.153.18.96:8080/')], contextPath: null, war: '**/*.war'
            }
        }
    }
}