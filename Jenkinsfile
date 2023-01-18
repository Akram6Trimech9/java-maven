//CODE_CHANGES=getGitChanges()
pipeline {
    agent any
    environment {
        NEW_VERSION = '1.3.0'
       // SERVER_CREDENTIALS= credentials(' ') //using credential plugin 
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        stage("build jar") {
            steps {
                script {
                    echo "building jar ${NEW_VERSION}"
                    //gv.buildJar()
                } 
            }
        }
        stage("test") {
            when {
                expression {
                   BRANCH_NAME == 'dev'|| RANCH_NAME == 'main' && CODE_CHANGES == true
                 }
            }
            steps { 
               echo 'testing the application .. '
            }
        }    
        stage("build image") {
            steps {
                script {
                    echo "building image"
                    //gv.buildImage()
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    echo "deploying"
                    //gv.deployApp()
                }
            }
        }
    }
    post { 
        always { 
        }
        success { 
        }
        failure { 
        }
        
    }
}
