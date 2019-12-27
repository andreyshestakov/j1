pipeline {
  agent any
  parameters {
    string(name: 'inventory_content', defaultValue: '127.0.0.1', description: 'Comma-separated host list')
  }
  stages {
    stage('Get facts') {
      steps {
        ansiblePlaybook(playbook: 'facts.yaml', colorized: true, inventoryContent: '192.168.43.19', disableHostKeyChecking: true, credentialsId: 'andres')
        archiveArtifacts 'out/facts.json'
      }
    }

    stage('libvirt') {
      steps {
        ansiblePlaybook(playbook: 'libvirt.yaml', become: true, colorized: true, credentialsId: 'andres', disableHostKeyChecking: true, inventoryContent: '192.168.43.19')
      }
    }

  }
}
