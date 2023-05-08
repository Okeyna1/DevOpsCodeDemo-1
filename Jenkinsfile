        pipeline{
            tools{
                jdk 'myjava'
                maven 'mymaven'
            }
            agent none
            stages{
                stage('Checkout'){
                    agent {label 'slave4'}
                    steps{
                echo 'cloning...'
                        git 'https://github.com/Okeyna1/DevOpsCodeDemo-1.git'
                    }
                }
                stage('Compile'){
                    agent {label 'slave1'}
                    steps{
                        echo 'compiling...'
                        sh 'mvn compile'
                }
                }
                stage('CodeReview'){
                    agent {label 'slave2'}
                    steps{
                    
                echo 'codeReview...'
                        sh 'mvn pmd:pmd'
                    }
                }
                stage('UnitTest'){
                    agent {label 'slave3'}
                    steps{
                    echo 'Testing'
                        sh 'mvn test'
                    }
                    post {
                    success {
                        junit 'target/surefire-reports/*.xml'
                    }
                }	
                }
                stage('Package'){
                    agent any
                    steps{
                        sh 'mvn package'
                    }
                }
            }
        }
