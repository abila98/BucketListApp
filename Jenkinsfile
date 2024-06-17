pipeline {
    agent any
    
    environment {
        ANT_HOME = '/usr/share/ant/bin' 
        AWS_CREDENTIALS = credentials('aws-credentials-id') 
        AWS_REGION = 'us-west-1' 
    }
    
    tools {
        ant 'Ant'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/abila98/BucketListApp.git', branch: 'main', credentialsId: 'github-credentials'
            }
        }

        stage('Build') {
            steps {
                // Run the Ant build using a shell command
                sh '''
                    # Run the Ant build
                    ant -f build.xml package
                '''
            }
        }
        
        stage('Package') {
            steps {
                // Run the Ant build using a shell command
                sh '''
                   aws s3 cp war/bucketlist.war s3://abilabucketlist/bucketlist.war
                '''
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed!'
        }
        always {
            // This will always run after the build, regardless of success or failure
            echo 'Build finished!'
        }
    }
}

