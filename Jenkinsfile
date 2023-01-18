pipeline {
    agent any
    tools {
        jdk 'JDK_8'
        jdk 'JDK_17'
        maven 'maven3'
    }
    parameters {
        choice(name: 'branch', choices: ['2.10', '2.11'], description: 'Choose the branch to build')
    }
    stages {
        stage ('Cloning Git'){
            steps{
        checkout([$class: 'GitSCM', branches: [[name: "*/${params.branch}"]], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/mydemo-apps/multi-java-pipe.git']]])

            }
        } 
        stage('Build Branch 2.10') {
            when {
                expression { params.branch == '2.10' }
            }
            steps {
                withEnv(["JAVA_HOME=${tool 'JDK_8'}"]) {
                withEnv(["MAVEN_HOME=${tool 'maven3'}", "PATH+MAVEN=${tool 'maven3'}/bin"]) {
                    sh 'mvn clean package'
                }
                }
            }
        }
        stage('Build Branch 2.11') {
            when {
                expression { params.branch == '2.11' }
            }
            steps {
                withEnv(["JAVA_HOME=${tool 'JDK_17'}"]) {
                withEnv(["MAVEN_HOME=${tool 'maven3'}", "PATH+MAVEN=${tool 'maven3'}/bin"]) {
                    sh 'mvn clean package'
                }
            }
        }
    }
}
}
