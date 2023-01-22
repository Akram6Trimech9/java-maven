//CODE_CHANGES=getGitChanges()
pipeline {
    agent any
    environment {
        NEW_VERSION = '1.3.0'
        SERVER_CREDENTIALS= credentials('server-credentials') //using credential plugin 
    }
    tools { 
    //build toools maven / gradle /jdk V71 /preinstalled in jenkins
        maven 'MAVEN'
    }
    parameters {
    //select which version 
        string ( name :'VERSION',defaultValue:'',description:'version to deploy on prod')
        choice( name :'version',choices:['fds','fdsf'] ) 
        booleanParam(name:'executeTests',defaultValue:true,description:'')
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
                   BRANCH_NAME == 'dev'|| RANCH_NAME == 'main' && CODE_CHANGES == true && params.executeTests
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
                    echo "deploying ${SERVER_CREDENTIALS}"
                    //withCredentials([
                       //usernamePassword(credentials :'server-credentials',usernamVariable:user,passwwordVariable:pwd') ]) 
                    //
                    ///sh "some script ${user} ${pwd)
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
