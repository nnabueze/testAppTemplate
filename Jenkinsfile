pipeline{
    agent{
        label "master"
    }
    environment{
        commitId = ''
    }
    stages{
        stage("Update Git"){
            steps{
                echo "======== Updating Git========"
                
                withCredentials([usernamePassword(credentialsId: 'Github', passwordVariable: 'pass', usernameVariable: 'user')]) {
                    echo 'password: ${pass}'
                    sh "git config user.email villa@gmail.com"
                    sh "git config user.name villa"
                    sh "cat deployment.yaml"
                    sh "sed -i 's+villavelle101/maths.*+villavelle101/maths:${params.DOCKERTAG}+g' deployment.yaml"
                    sh "cat deployment.yaml"
                    sh "git add ."
                    sh "git commit -am 'Triggered Build: ${env.BUILD_NUMBER}'"
                    sh "git push https://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@github.com/${user}/testAppTemplate.git HEAD:master"
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