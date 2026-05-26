pipeline {
    agent any

    stages {

        stage('Clone Repository') {
            steps {
                git branch: 'main', url: 'https://github.com/JAYAKAVITHA10/multi-cloud-dr-project.git'
            }
        }

        stage('Deploy to AWS') {
            steps {
                sh '''
                scp html/index-aws.html ubuntu@10.0.1.235:/tmp/index.html

                ssh ubuntu@10.0.1.235 "
                sudo apt update -y &&
                sudo apt install nginx -y &&
                sudo mkdir -p /var/www/html &&
                sudo cp /tmp/index.html /var/www/html/index.html &&
                sudo systemctl enable nginx &&
                sudo systemctl restart nginx
                "
                '''
            }
        }

        stage('Deploy to Azure') {
            steps {
                sh '''
                scp html/index-azure.html azureuser@13.82.144.159:/tmp/index.html 

                ssh azureuser@13.82.144.159 " 
                sudo apt update -y &&
                sudo apt install nginx -y &&
                sudo mkdir -p /var/www/html &&
                sudo cp /tmp/index.html /var/www/html/index.html &&
                sudo systemctl enable nginx &&
                sudo systemctl restart nginx
                "
                '''
            }
        }
    }
}