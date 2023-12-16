pipeline{
    agent any
    tools{
        maven 'Maven'
    }
    stages{
        stage("Test"){
            steps{
                //mvn test
                echo "Testing......."
                sh 'mvn test'
            }
        }
        stage("Build"){
            steps{
                //mvn package
                echo "Building....."
                sh 'mvn package'
            }
        }
        stage("Deploy on Mock Server"){
            steps{
                //deploy on container -> plugin
                echo "Deploying on mock server........"
                deploy adapters: [tomcat9(credentialsId: 'newID2', path: '', url: 'http://65.1.91.110:8080')], contextPath: '/myApp', war: '**/*.war'
                
            }
        }
        stage("Deploy on Production Server"){ 
            input{
                message "Should we continue?"
                ok "Yes we should"
            }
            
            steps{
                echo "Deploying on Production Server......."
                //deploy on container -> plugin
                deploy adapters: [tomcat9(credentialsId: 'newID2', path: '', url: 'http://13.233.142.124:8080')], contextPath: '/myApp', war: '**/*.war'
            
                
            }
        }
    }
    post{
        always{
            echo "_______________Always_______________"

        }
        success{
                echo "________________Success___________________"
        }
        failure{
                echo "______________Failure________________"
        }
    }
}
