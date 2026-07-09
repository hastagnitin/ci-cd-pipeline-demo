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
                
                echo "installing Apache"
                
                
                    sudo yum install httpd -y
                    sudo mkdir -p /var/www/html
                    sudo cp index.html /var/www/html/
                    sudo systemctl start httpd
                    sudo systemctl stop firewalld
                '''
            }
        }
    }
}