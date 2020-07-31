import java.text.SimpleDateFormat
import groovy.transform.Field
@Library('jenkins-pipeline-utils') _

node {
    try {
        stage('Preparation') {
            checkout([$class: 'GitSCM', branches: [[name: '$branch']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'f10a8cc7-7ebf-4dc1-9ad4-2a8b37c8edec', refspec: '$refspec', url: 'git@github.com:vreddy-devops/helloworld.git']]])
        }
    }
    catch (err) {
        currentBuild.result = 'FAILED'
        throw err
    }

}
