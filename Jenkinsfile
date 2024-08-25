def registry = 'https://harpal555.jfrog.io/'

pipeline {
    agent any

    environment {
        PATH = "/opt/maven/bin:$PATH"
    }

    stages {
        stage("build") {
            steps {
                echo "----------- build started ----------"
                sh 'mvn clean deploy -Dmaven.test.skip=true'
                echo "----------- build completed ----------"
            }
        }

        stage("test") {
            steps {
                echo "----------- unit test started ----------"
                sh 'mvn surefire-report:report'
                echo "----------- unit test completed ----------"
            }
        }

        stage('SonarQube analysis') {
            environment {
                scannerHome = tool 'Sonar-Qube'
            }
            steps {
                withSonarQubeEnv('Sonar-Qube') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
    }
}

