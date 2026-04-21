node {
    checkout scm

    def PROD_HOST = '127.0.0.1'
    def DEPLOY_PATH = '/home/carl/deploy-laravel'
    def DEPLOY_USER = 'carl'

    stage('Info') {
        sh 'pwd'
        sh 'ls'
        sh 'ls app'
        sh 'ls routes'
        sh 'cat composer.json | head'
    }

    stage('Build') {
        sh '''
            echo "Build stage"
            mkdir -p build_output
            cp -r app bootstrap config database public resources routes storage tests artisan composer.json composer.lock package.json phpunit.xml vite.config.js README.md .env.example build_output/ 2>/dev/null || true
            ls build_output
        '''
    }

    stage('Test') {
        sh '''
            echo "Test stage"
            test -f artisan
            test -f composer.json
            test -d app
            test -d routes
            echo "Laravel source structure OK"
        '''
    }

    stage('Deploy') {
        sshagent(['ssh-prod']) {
            sh """
                echo "Deploy stage"
                ssh -o StrictHostKeyChecking=no ${DEPLOY_USER}@${PROD_HOST} "mkdir -p ${DEPLOY_PATH}"
                rsync -av --delete -e "ssh -o StrictHostKeyChecking=no" ./ ${DEPLOY_USER}@${PROD_HOST}:${DEPLOY_PATH}/
            """
        }
    }

    stage('Verify') {
        sshagent(['ssh-prod']) {
            sh """
                ssh -o StrictHostKeyChecking=no ${DEPLOY_USER}@${PROD_HOST} "ls -la ${DEPLOY_PATH} && test -f ${DEPLOY_PATH}/artisan && echo DEPLOY_OK"
            """
        }
    }
}
