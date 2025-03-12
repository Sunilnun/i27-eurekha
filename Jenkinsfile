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
        SONAR_TOKEN = credentials('sonar')
        SONAR_URL = "http://34.72.64.46:9000 "
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
                echo "starting sonar scan"
                withSonarQubeENV('sonar'){//the name you saved in syatem under configure jenkins
                sh """
                echo "starting sonar scan"
                mvn sonar:sonar\
                    -Dsonar.projectkey=i27-eureka \
                    -Dsonar.host.url= ${env.SOANR_URL}\
                    -Dsonar.login= ${SONAR_TOKEN}
                """
                }
                timeout(time:2 , unit: 'MINUTES'){
                    waitForQualityGate abortPipeline: true
                }
            
                
            }

        }
    }
}
