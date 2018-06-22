pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                echo "Check out gitlab"
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/master']],
                    doGenerateSubmoduleConfigurations: false,
                    extensions: [],
                    submoduleCfg: [],
                    userRemoteConfigs: [[
                        credentialsId: '0acb57ef-daed-48ea-8ca4-0b82cce3cd32',
                        url: 'https://github.com/luckyfoto/demo-test-build-docker.git'
                    ]]
                ])
            }
        }

        stage ('Unit Test') {
            steps {
                echo "Run Unit Test"
                sh "${tool 'M3'}/bin/mvn -U clean test package -Dspring.profiles.active=${env.profilesActive}"
            }
        }

        stage ('Build Docker Image') {
            steps {
                echo "Building JAR"
                sh "${tool 'M3'}/bin/mvn package docker:build -Dmaven.test.skip=true"
            }
        }

        stage ('Verify Docker Image') {
            steps {
                echo "Verify"
            }
        }

        stage ('Push Docker Image') {
            steps {
                echo "Uploading"
            }
        }
    }
}
