pipeline {
   agent any
   
   stages {
       stage('Checkout') {
           steps {
               checkout([$class: 'GitSCM',
                         branches: [[name: '*/master']],
                         doGenerateSubmoduleConfigurations: false,
                         extensions: [],
                         submoduleCfg: [],
                         userRemoteConfigs: [[url: 'https://github.com/ninjaxmen/DEVOPS.git']]
                      ])
           }
       }
       
       stage('Build') {
           steps {
               sh 'mvn clean package'
           }
       }
       
       stage('Deploy') {
           steps {
               deploy(
                 adapters: [tomcat8(
                             credentialsId: 'tomcat-creds',
                             url: 'http://localhost:8080',
                             path: '/myapp',
                             contextPath: '/myapp'
                          )],
                 war: '**/target/*.war'
               )
           }
       }
   }
   
   post {
       always {
           cleanWs()
       }
   }
}
