pipeline  {
    agent { label 'JDK_8' }
    triggers { pollSCM '* * * * *' }
    stages {
        stage('vcs') {
            steps {
                git url: 'https://github.com/qtrajkumarmarch23/game-of-life.git',
                    branch: 'master'
            }
        }
        stage('package') {
            steps {
                sh 'export PATH="/usr/lib/jvm/java-1.8.0-openjdk-amd64/bin:$PATH" && 'mvn package''
            }
        }
        stage('post build') {
            steps {
                archiveArtifacts artifacts: '**/target/game-of-life.war',
                                 onlyIfSuccessful: true
                junit testResults: '**/surefire-reports/TEST-*.xml'                 
            }
        }
    }
}