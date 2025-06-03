- name: Deploy Maven Artifact
  hosts: localhost
  tasks:
    - name: Copy JAR to deploy directory
      copy:
        src: /mnt/c/ProgramData/Jenkins/.jenkins/jobs/proj2/builds/4/archive/target/cicdproject-0.0.1-SNAPSHOT.jar 
        dest: /home/shank/deploy/
------------------------------------------------------------------------------------------------------------------------
pipeline {
agent any
stages {
stage('Checkout') {
steps {
git branch: 'main', url: 'https://github.com/ShashankRaghuram1509/Proj2.git'
}
}
stage('Build') {
steps {
bat 'mvn clean install'
}
}
stage('Archive Artifact') {
steps {
archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
}
}
}
}
