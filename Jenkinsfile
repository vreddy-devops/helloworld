DOCKER_GROUP = 'vinodtaborda'
DOCKER_IMAGE = 'helloworld'
DOCKER_REGISTRY_CREDENTIALS_ID = 'c1b47731-842a-475c-adb9-69c94ff40f1d'
DOCKER_CONTAINER_NAME = 'HelloWorld'
GIT_URL = 'git@github.com:vreddy-devops/helloworld.git'
GIT_CREDENTIALS_ID = '3a6ccec5-111d-41b5-9360-83afd9d02528'
node {
    def app
    try {
        stage('Preparation') {
            // checkout scm
            checkout(
                [
                    $class: 'GitSCM', 
                    branches: [[name: 'pipeline']], 
                    doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], 
                    userRemoteConfigs: [
                        [
                            credentialsId: GIT_CREDENTIALS_ID, 
                            url: GIT_URL
                        ]
                    ]
                ]
            )
        }
        stage('Build Docker Image') {
            app = docker.build("${DOCKER_GROUP}/${DOCKER_IMAGE}:${env.BUILD_ID}")
        }
        stage('Publish Image') {
            withDockerRegistry([credentialsId: DOCKER_REGISTRY_CREDENTIALS_ID]) {
                app.push()
                app.push('latest')
            }
        }
        // stage('Deploy') {
        //     sh "docker rm $(docker ps --all --quiet)"
        //     sh "docker rm $(docker ps --quiet --filter status=exited)"
        //     withDockerRegistry([credentialsId: DOCKER_REGISTRY_CREDENTIALS_ID]) {
        //         sh "docker pull ${DOCKER_GROUP}/${DOCKER_IMAGE}"
        //         sh "docker run --detach --publish 80:3000 --name ${DOCKER_CONTAINER_NAME} ${DOCKER_GROUP}/${DOCKER_IMAGE}"
        //     }
        // }
        stage('Clean Up') {
            sh "docker images ${DOCKER_GROUP}/${DOCKER_IMAGE} --filter \"before=${DOCKER_GROUP}/${DOCKER_IMAGE}:${env.BUILD_ID}\" -q | xargs docker rmi -f || true"
        }
    } 
    catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    } 
    finally {
        cleanWs()
    }
}
