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
