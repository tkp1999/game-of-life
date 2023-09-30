pipeline{
    agent{
        label 'JDK_8'
    }
    options{
        retry(3)
        timeout(time: 60, unit: 'MINUTES')
    }
    triggers{
        pollSCM('* * * * *')
    }
    tools{
        maven 'maven3.9'
        jdk 'JAVA_8'
    }
    stages{
        stage('get code from github'){
            steps{
                git branch: 'master',
                    url: 'https://github.com/tkp1999/game-of-life.git'

            }
        }
        stage('build and package'){
            steps{
                sh script: '/usr/share/maven/apache-maven-3.9.4/bin/mvn clean package'

            }
        }
        stage('reporting'){
            steps{
                junit testResults: '**/surefire-reports/TEST-*.xml'
                archiveArtifacts artifacts: '**/gameoflife.war'

            }
        }
    }
}