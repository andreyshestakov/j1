pipeline {
  agent any
  parameters {
    string(name: 'INVENTORY_CONTENT', defaultValue: '127.0.0.1', description: 'Comma-separated host list')
    choice(choices: 'andres', description: "credentialsId", name: 'CREDENTIALS_ID')
  }
  stages {
    stage('Get facts') {
      steps {
        ansiblePlaybook(playbook: 'facts.yaml', colorized: true, inventoryContent: params.INVENTORY_CONTENT, disableHostKeyChecking: true, credentialsId: params.CREDENTIALS_ID)
        archiveArtifacts 'out/facts.json'
      }
    }

    stage('libvirt') {
      steps {
        ansiblePlaybook(playbook: 'libvirt.yaml', become: true, colorized: true, credentialsId: params.CREDENTIALS_ID, disableHostKeyChecking: true, inventoryContent: params.INVENTORY_CONTENT)
      }
    }

  }
}
