pipeline {
  agent any
   
       tools {
  // No valid tools specified
         maven 'maven'
      }
   stages{
   stage('checkout scm'){
        steps{
         checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'vij-gitea', url: 'http://localhost:3000/vijay_gitea/Covid_scripting.git']]])
        }
        }
   stage('build '){
            steps{
                sh 'mvn clean install -f pom.xml'
            }

  }
  stage('deploy war')
        {
           steps{
           deploy adapters: [tomcat8(credentialsId: 'tomcat-cred', path: '', url: 'http://localhost:5050/manager/')], contextPath: 'scripted', war: '**/*.war'
        
        }
        }
    stage('invoking ansible-playbook')
    {
    steps{ansiblePlaybook installation: 'ansible', inventory: '/var/lib/jenkins/workspace/covid-Vaccine-job1/inventory.inv', playbook: '/var/lib/jenkins/workspace/covid-scripting/cap.yml'}
}
        }}

