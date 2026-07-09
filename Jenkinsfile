pipeline {
    agent any
    stages {

        stage ('Checkout Source Code') {
            steps {
                checkout scm
            }
        }

        stage ('Deploy to testing server') {
            steps {
                echo "Installing Apache on Testing Server"
                sh '''
                sudo yum install httpd -y
                sudo mkdir -p /var/www/html
                sudo cp index.html /var/www/html/
                sudo systemctl start httpd
                sudo systemctl stop firewalld
                '''
            }
        }

        stage ('Technical Team Approval') {
            steps {
                input (
                    message: 'Technical Team, is Testing Successful?',
                    ok: 'Approve Deployment'
                )
            }
        }

        stage ('Deploy to Production') {
            steps {
                echo "Deploying to Production Server"
                sh '''
                sudo yum install httpd -y
                sudo mkdir -p /var/www/html
                sudo cp index.html /var/www/html/
                sudo systemctl start httpd
                sudo systemctl stop firewalld
                '''
            }
        }

        stage ('Manager Approval') {
            steps {
                input (
                    message: 'Manager, Approve Production Release?',
                    ok: 'Release'
                )
            }
        }

        stage ('Production release complete') {
            steps {
                echo "Application Successfully Deployed BY Jenkins"
            }
        }
    }

    
    post {
        success {
            mail(
                to: 'nitin978032@gmail.com',
                subject: 'Production Deployment Successfully Done',
                body: "Hello Team,\n\nProduction Deployment done.\n\nAll stages worked."
            )
        }
        failure {
            mail(
                to: 'nitin978032@gmail.com',
                subject: 'Production Deployment Failed',
                body: "Hello Team,\n\nProduction Deployment failed.\n\nPlease check the Jenkins logs."
            )
        }
    }
}