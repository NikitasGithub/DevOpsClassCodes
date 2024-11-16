pipeline {
    agent any
    
    tools{
        maven "mymaven"
    }

    stages {
        stage('CloneRepo') {
            steps {
                echo 'This is stage1'
                git 'https://github.com/NikitasGithub/DevOpsClassCodes.git'
            }
        }
        
         stage('Compile') {
            steps {
                bat 'mvn compile'
            }
        }
        
        stage('CodeReview') {
            steps {
                bat 'mvn pmd:pmd'
            }
            post{
                success{
                   recordIssues(tools: [pmdParser(pattern: '**/pmd.xml')]) 
                }
            }
        }
        
         stage('test') {
            steps {
                bat 'mvn test'
            }
            post{
                success{
                   junit 'target/surefire-reports/*.xml'
                }
            }
        }
        
        stage('package') {
            steps {
                bat 'mvn package'
            }
        }
    }
}
