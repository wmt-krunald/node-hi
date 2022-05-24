pipeline {
    agent any
 
    tools {nodejs "node"}

    environment {
        CI = 'true'
    }

    stages{

        stage('check') {
            steps {
            sh 'npm config ls'
            }
        }

        stage('build') {
            steps {
                sh 'npm i'
                sh 'npm run build'
            }
        }

        // stage('start') {
        //     steps {
        //         sh 'npm run start'
        //     }
        // }
        stage('deploy') {
            environment {
                NETLIFY_AUTH_TOKEN = credentials('NETLIFY_AUTH_TOKEN')
                NETLIFY_SITE_ID = credentials('NETLIFY_SITE_ID')
            }
            
            steps {
                sh 'npm install netlify-cli'
                sh 'npx netlify deploy --site $NETLIFY_SITE_ID --auth $NETLIFY_AUTH_TOKEN --dir build/ --prod'
                echo "Running Build URl: ${env.BUILD_URL}"
                echo "Running JOB_DISPLAY_URL: ${env.JOB_DISPLAY_URL}"
                echo "Running JOB_URL: ${env.JOB_URL}"
                echo "Running JENKINS_URL: ${env.JENKINS_URL}"
            }
        }
    }

}