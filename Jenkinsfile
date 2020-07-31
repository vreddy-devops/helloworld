DOCKER_GROUP = 'vinodtaborda'
DOCKER_IMAGE = 'helloworld'
DOCKER_REGISTRY_CREDENTIALS_ID = 'c1b47731-842a-475c-adb9-69c94ff40f1d'
node {
    def app
    try {
        stage('Preparation') {
            checkout scm
            // checkout([$class: 'GitSCM', branches: [[name: 'pipeline']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'f10a8cc7-7ebf-4dc1-9ad4-2a8b37c8edec', url: 'git@github.com:vreddy-devops/helloworld.git']]])
        }
        stage('Build Docker Image') {
            app = docker.build("${DOCKER_GROUP}/${DOCKER_IMAGE}:${env.BUILD_ID}")
        }
    }
    catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }

}
