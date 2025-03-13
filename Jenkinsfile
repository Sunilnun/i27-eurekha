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
        POM_VERSION = readMavenPom().getVersion()
        POM_PACKAGING = readMavenPom().getPackaging()

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
                // withSonarQubeENV('sonar'){//the name you saved in syatem under configure jenkins
                sh """
                echo "starting sonar scan"
                mvn sonar:sonar\
                    -Dsonar.projectkey=i27-eureka \
                    -Dsonar.host.url= ${env.SOANR_URL}\
                    -Dsonar.login= ${SONAR_TOKEN}
                """
                }
                // timeout(time:2 , unit: 'MINUTES'){
                //     waitForQualityGate abortPipeline: true
                // }
            
                
            }

        
        stage('Docker'){
            steps{
                //existing artifact image format: i27-eurekha-0.0.1-snapshot.jar
                //My destination artifact image format : i27-eurekha-buildnumber-branchname.jar
                //if any errors with readmepom, make sure pipeline-utility-steps plugin is installed in yourjenkins if not install the plugin
                //when ever we are running the scripts we need to approve the scrits. it is a one time activity
                //http://35.231.34.185:8080/scriptapproval/
                echo "My JAR source : i27-${env.APPLICATION_NAME}-${env.POM_VERSION}.${env.POM_PACKAGING}"
                echo "MY JAR destination: i27-${env.APPLICATION_NAME}-${BUILD_NUMBER}-${BRANCH_NAME}.${env.POM_PACKAGING}"
                sh """
                echo "******Building the docker image********"

                pwd
                ls-la
                """

            }
        }
    }
}
