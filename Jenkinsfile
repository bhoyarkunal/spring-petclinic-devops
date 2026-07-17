pipeline {
    agent{label 'SPC'}
    triggers{
        pollSCM("* * * * *")
    }
    stages {
        stage('git checkout'){
            steps{
                git url: 'https://github.com/bhoyarkunal/spring-petclinic-devops.git',
                branch: 'main'
            }
        }
        stage('scan'){
            steps {
                withCredentails([string(withCredentailsId: 'ids_12', variable: 'SONAR_TOKEN')]){
                withSonarQubeEnv('SONAR'){
                sh """mvn clean verify sonar:sonar \
                -Dsonar.projectKey=bhoyarkunal_spring-petclinic-devops \
                -Dsonar.organization=bhoyarkunal \
                -Dsonar.host.url=https://sonarcloud.io/ \
                -Dsonar.login=SONAR_TOKEN"""
            }

            }
        }

    }
}
}
