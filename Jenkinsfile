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
                echo "Building the ${env.APPLICATION_NAME} application"
                sh 'mvn clean package -DskipTests=true'         
            }           
        }
        stage('sonar'){
            steps{
                sh """
                echo"starting sonar scan"
                mvn sonar:sonar\
                    -Dsonar.projectkey=i27-eureka \
                    -Dsonar.host.url=http://34.72.64.46:9000 \
                    -Dsonar.login=squ_50068d6ce761445864e22d81feae3bf1d6773f84
                """
            }

        }
    }
}
