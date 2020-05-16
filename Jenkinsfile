#!groovy
pipeline {
    options {
        timeout(time: 1, unit: 'HOURS')
    }
    agent any
    stages {
        stage('build docker ') {
            steps {
                dir('docker') {
                    script {
                        if (env.BRANCH_NAME == 'master') {
                            latestTag = sh(returnStdout: true, script: "git describe --tags --abbrev=0").trim()
                            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                                def customImage = docker.build("saja/reverseproxy:${latestTag}")
                                customImage.push()
                            }
                        }
                    }
                }
            }
        }
    }
}
