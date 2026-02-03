pipeline {
  agent any

  stages {
    stage('GitHub') {
      steps {
        git branch: 'main', url: 'https://github.com/DEEPIKA-B-29/chatapp-modified-ubuntu-22.04.git'
      }
    }

    stage('Deploy') {
      steps {
        sh '''

          rsync -avz --exclude='.git/' "$WORKSPACE"/* jenkins@10.0.177.140:/tmp/chatapp/
          ssh jenkins@10.0.177.140 'sudo -u chatapp cp -rfv /tmp/chatapp/fundoo /app/'
          ssh jenkins@10.0.177.140 'sudo -u chatapp cp -fv /tmp/chatapp/requirements.txt /app/'
          ssh jenkins@10.0.177.140 'sudo -u chatapp /usr/local/bin/chatapp_deploy.sh'
        '''
      }
    }
  }

  post {
    success { echo 'Deploy completed successfully' }
    failure { echo 'Deploy failed — check logs above' }
  }
}
