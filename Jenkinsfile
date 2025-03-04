pipeline{
    agent {
        label 'k8s-slave'
    }
    tools {
        maven 'Maven-3.8.8'
        jdk 'JDK-17'

    }
    environment {
        APPLICATION_NAME = "eurekha"
    }

    //stages
    stages{
        stage('build'){
            steps{
                echo "Building the ${env.APPLICATION_NMAE} application"
                sh 'mvn clean package -DskipTests=true'
            

            }
            

        }
    }
}
