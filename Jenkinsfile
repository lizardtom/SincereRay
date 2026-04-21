node {
    checkout scm

    stage('Info') {
        sh 'pwd'
        sh 'ls'
        sh 'ls app'
        sh 'ls routes'
        sh 'cat composer.json | head'
    }

    stage('Build') {
        echo 'Build stage'
    }

    stage('Test') {
        echo 'Test stage'
    }

    stage('Deploy') {
        echo 'Deploy stage'
    }
}
