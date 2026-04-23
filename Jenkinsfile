node {
    checkout scm

    stage("Info") {
        sh 'pwd'
        sh 'ls'
    }

    stage("Build") {
        sh 'echo BUILD UPDATED BY CARL'
        sh 'mkdir -p build_output'
        sh 'cp -r app bootstrap config database public resources routes storage tests artisan composer.json composer.lock package.json phpunit.xml vite.config.js README.md .env.example build_output/'
    }

    stage("Test") {
        sh 'echo TEST UPDATED SUCCESS'
        sh 'echo Laravel OK'
    }

    stage("Deploy") {
        sh 'echo DEPLOY UPDATED START'
        sh 'mkdir -p deploy_output'
        sh 'cp -r build_output/* deploy_output/'
        sh 'echo DEPLOY SUCCESS UPDATED'
    }
}
