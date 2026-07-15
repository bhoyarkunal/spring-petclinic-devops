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
        stage('build'){
            steps {
                sh "mvn package"
            }
        }

    }
}

























