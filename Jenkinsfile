pipeline {
    agent any
    tools {
        maven 'maven 3.8.6'
        jdk 'JDK 11'
    }
    stages {
        stage("Tools initialization") {
            steps {
                sh "mvn --version"
                sh "java -version"
            }
        }
        stage("Checkout Code") {
            steps {
                checkout scm
            }
        }
        stage("Check Code Health") {
            when {
                not {
                    anyOf {
                        branch 'master';
                        branch 'develop'
                    }
                }
           }
           steps {
               echo 'master code health'
            }
        }
        stage("Run Test cases") {
            when {
                branch 'develop';
            }
           steps {
               echo 'master test'
            }
        }
        stage("Check Code coverage") {
            when {
                branch 'develop'
            }
            steps {
               jacoco(
                    execPattern: '**/target/**.exec',
                    classPattern: '**/target/classes',
                    sourcePattern: '**/src',
                    inclusionPattern: 'com/iamvickyav/**',
                    changeBuildStatus: true,
                    minimumInstructionCoverage: '30',
                    maximumInstructionCoverage: '80')
           }
        }
        stage("Build & Deploy Code") {
            when {
                branch 'master'
            }
            steps {
                echo 'master deploy'
            }
        }
    }
 }
