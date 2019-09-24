node {
    stage ('Checkout Repository') {
        deleteDir()
        checkout scm
        // Get our repo cloned and prepped for action
    }

    stage ('Render Configurations') {
        sh 'ansible-playbook generate_configurations.yaml'
        // Generate configs with playbooks
    }

    stage ('Unit Testing') {
        // Do Linting
    }

    stage ('Deploy Configs to Dev') {
        sh 'python3 -m venv jenkins_build'
        sh 'jenkins_build/bin/python -m pip install -r requirements.txt'
        sh 'git clone https://github.com/luylaki/napalm_ansible'
        sh 'cp -r napalm-ansible/napalm_ansible/ jenkins_build/lib/python3.6/site-packages/'
        sh 'jenkins_build/bin/python napalm-ansible/setup.py install'
        sh '''sed -i -e 's/\\/usr\\/local/jenkins_build/g' ansible.cfg'''
        sh '''sed -i -e 's/dist-/site-/g' ansible.cfg'''
        sh '''sed -i -e 's/\\/usr\\/bin/jenkins_build\\/bin/g' ansible.cfg'''
        sh 'ansible-playbook deploy_configurations.yaml -e "ansible_python_interpreter=jenkins_build/bin/python"'
        // Push configs to Dev
    }

    stage ('Functional/Integration Testing') {
        // Ping stuff and check dev env
    }

    stage ('Promote Configurations to Production') {
        // Ping and Test
    }

    stage ('Production Functional/Integration Testing') {
        // More Ping and Test
    }
}
