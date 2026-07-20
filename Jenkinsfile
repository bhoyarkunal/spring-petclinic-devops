pipeline {
    agent {
        label 'JAVASPC'
    }

    triggers {
        pollSCM('* * * * *')
    }

    stages {

        stage('Git Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/bhoyarkunal/spring-petclinic-devops.git'
            }
        }

        stage('Scan') {
            steps {
                withCredentials([string(credentialsId: 'sonar_12', variable: 'SONAR_TOKEN')]) {
                    withSonarQubeEnv('SONAR') {
                        sh """
                            mvn clean verify sonar:sonar \
                            -Dsonar.projectKey=bhoyarkunal_spring-petclinic-devops \
                            -Dsonar.organization=bhoyarkunal \
                            -Dsonar.host.url=https://sonarcloud.io \
                            -Dsonar.login=$SONAR_TOKEN
                        """
                    }
                }
            }
        }

        stage('upload binaryfile'){
            steps{
                    rtUpload(
                        serverId: 'JFRONG_ID',
                        spec: '''{
                        "files":[
                        {
                        "pattern":"target/*.jar",
                        "target": "javaspc/"
                        }
                        ]
                        }'''
                    )
                   rtPublishBuildInfo(serverId:'JFRONG_ID') 
            }
        }
    }
}









