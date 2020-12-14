pipeline {
    agent any
    stages {
        stage ('Build Backend'){
            steps{
                bat 'mvn clean package -DskipTests=true'
            }
        }
        stage ('Unit Tests'){
            steps{
                bat 'mvn test'
            }
        }
        stage ('Sonar Analysis'){
            environment{
                scammerHome = tool 'SONAR`_SCANNER'
            }
            steps{
                withSonarQubeEnv('SONAR_LOCAL'){
                    bat "${scammerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://localhost:9000 -Dsonar.login=16e47102b52570b80050e8021f7631e941808eb0 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn/**,**/src/test/**,**/model/**,**Application.java"
                }
            }
        }
    }
}