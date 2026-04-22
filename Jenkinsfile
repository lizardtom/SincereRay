node {
    checkout scm

    stage("Info") {
        sh 'pwd'
        sh 'ls'
        sh 'ls app'
        sh 'ls routes'
        sh 'cat composer.json | head'
    }

    stage("Build") {
        sh 'echo Build stage'
        sh 'mkdir -p build_output'
        sh 'cp -r app bootstrap config database public resources routes storage tests artisan composer.json composer.lock package.json phpunit.xml vite.config.js README.md .env.example build_output/'
        sh 'ls build_output'
    }

    stage("Test") {
        sh 'echo Test stage'
        sh 'test -f artisan'
        sh 'test -f composer.json'
        sh 'test -d app'
        sh 'test -d routes'
        sh 'echo Laravel source structure OK'
    }

    stage("Deploy") {
        sh 'echo Deploy stage'
        sh 'mkdir -p deploy_output'
        sh 'cp -r build_output/* deploy_output/'
        sh 'echo Deploy simulation success'
    }
}
