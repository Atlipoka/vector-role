pipeline {
    agent {
  label 'linux'
    }
    stages  {
        stage ('Check versions') {
            steps {
                sh 'ansible --version'
                sh 'molecule --version'  
            }
            
        }
        stage ('Prepate env') {
            steps {
                sh 'ssh-keyscan -t rsa github.com >> ~/.ssh/known_hosts'
                sh 'rm -rf * .travis.yml .yamllint .git'
                sh 'git clone -b 1.2.0 git@github.com:Atlipoka/vector-role.git .'
                sh 'git clone git@github.com:Atlipoka/vector-role.git'
                sh 'cp vector-role/requirements.yml .'
                sh 'ansible-galaxy install -r requirements.yml'
            }
        }
        stage ('Start molecule') {
            steps {
                sh 'molecule test -s default'
            }
        }
    }
}
