pipeline {
    agent { label 'MAVEN_JDK8' }
    triggers { pollSCM ('H/30 * * * *') }
    parameters {
        string(name: 'MAVEN_GOAL', defaultValue: 'package', description: 'Maven Goal')
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/khajadevopsmarch23/game-of-life.git',
                    branch: 'declarative'
            }
        }
        stage('package') {
            tools {
                jdk 'JDK_8_UBUNTU'
            }
            steps {
                sh "mvn ${params.MAVEN_GOAL}"
            }
        }
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/target/gameoflife.war',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'
            }
        }
    }
}