pipeline{
    agent{
        label "master"
    }
    stages{
        stage("Update Git"){
            steps{
                echo "======== Updating Git========"
                withCredentials([usernamePassword(credentialsId: 'Github', passwordVariable: 'gitHubToken', 
                usernameVariable: 'nnabueze')]) {
                    sh "git config user.email villa@gmail.com"
                    sh "git config user.name villa"
                    sh "cat deployment.yaml"
                    sh "sed -i 's+villavelle101/maths.*+villavelle101/maths:${DOCKERTAG}' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -m 'Triggered Build: ${env.BUILD_NUMBER}'"
                    sh "git push https://${nnabueze}:${gitHubToken}@github.com/${nnabueze}/testAppTemplate.git"
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