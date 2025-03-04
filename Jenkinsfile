pipeline{
    agent {
        label 'k8s-slave'
    }
    tools {
        maven 'Maven-3.8.8'
        jdk 'JDK-17'

    }
    environment {
        Application_name = "eurekha"
    }

    //stages
    stages{
        stage('build'){
            steps{
                echo "Building the ${env.Application_name} application"
                sh 'mvn clean package -DskipTests=true'
            

            }
            

        }
    }
}
