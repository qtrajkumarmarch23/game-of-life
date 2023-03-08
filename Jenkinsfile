pipeline {
    agent { label 'JDK_8' }
    triggers { pollSCM ('* * * * *') }
    parameters {
        choice(name: 'MAVEN_GOAL', choices: ['package', 'install', 'clean'], description: 'MAVEN_GOAL')
    }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/qtrajkumarmarch23/game-of-life.git',
                    branch: 'master'
            }
        }
        stage('package') {
            tools {
                jdk 'JDK_8'
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