pipeline {
    agent any
    environment {
        ANSIBLE_HOST = '172.31.25.202'        // The machine where Ansible is installed
        KUBECONFIG_PATH = '/home/ubuntu/.kube/config'    // Path to the Kubernetes kubeconfig file
    }
    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/your-repo.git'  // Fetch your codebase
            }
        }
        stage('Run Ansible Playbook') {
            steps {
                sshagent(['your-ssh-credentials-id']) {
                    sh '''
                    ansible-playbook -i ${ANSIBLE_HOST}, \
                                     -e kubeconfig_path=${KUBECONFIG_PATH} \
                                     ansible/deploy.yml  // Run the Ansible playbook
                    '''
                }
            }
        }
    }
    post {
        success {
            echo 'Deployment Successful!'
        }
        failure {
            echo 'Deployment Failed!'
        }
    }
}
