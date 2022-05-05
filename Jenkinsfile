pipeline{
    agent{
        label "master"
    }
    environment{
        secret = ''
    }
    stages{
        stage("Update Git"){
            steps{
                echo "======== Updating Git========"
                
                withCredentials([string(credentialsId: 'gitHubToken', variable: 'token')]) {
                    secret = URLEncoder.encode("$token",'UTF-8')
                    sh "git config user.email villa@gmail.com"
                    sh "git config user.name villa"
                    sh "cat deployment.yaml"
                    sh "sed -i 's+villavelle101/maths.*+villavelle101/maths:${params.DOCKERTAG}+g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -am 'Triggered Build: ${env.BUILD_NUMBER}'"
                    sh 'git push https://${secret}@github.com/nnabueze/testAppTemplate.git HEAD:master'
                }
            }
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}