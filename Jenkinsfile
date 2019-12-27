pipeline {
  agent any
  stages {
    stage('error') {
      steps {
        ansiblePlaybook(playbook: 'facts.yaml', colorized: true, inventoryContent: '192.168.43.19', disableHostKeyChecking: true, credentialsId: 'andres')
      }
    }

    stage('archive facts') {
      steps {
        archiveArtifacts 'out/facts.yaml'
      }
    }

    stage('libvirt') {
      steps {
        ansiblePlaybook(playbook: 'libvirt.yaml', become: true, colorized: true, credentialsId: 'andres', disableHostKeyChecking: true, inventoryContent: '192.168.43.19')
      }
    }

  }
}