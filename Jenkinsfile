def storage="/mnt/artifacts"
pipeline {
options {
 timeout(time: 30, unit: 'MINUTES')
}
agent { label 'master' }
 stages {
  stage('Checkout') {
   steps {
    script {
      deleteDir()
      dir ('INT_API') {
           checkout([$class: 'GitSCM', branches: [[name: '*/yuri']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'git_rd_cred', url: 'https://github.com/roz-Devops/INT_API.git']]])
           Commit_Id = '1.0.0'
     }
    }
   }
  }
  stage('Build') {
   steps {
    script {
      dir ('INT_API') {
           sh 'ls'
           sh 'pwd'
           sh "sudo docker build . -t intapi:${Commit_Id}"
     //take latesr version from prod.json and add commit id to it -- use this as dev version during the ci
     // add try catch
     }
    }
   }
  }
  stage('Save to docker image to repo') {
   steps {
    script {
     sh "sudo mkdir -p ${storage}/dev"
     sh "sudo docker save intapi:${Commit_Id} > ${storage}/dev/intapi_${Commit_Id}.tar"
     }
    }
   }
  }
}
