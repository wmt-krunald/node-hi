pipeline {
    agent any
    
    tools {nodejs "node"}

    environment {
        CI = 'true'
    }

    parameters{choice(choices:'master\nmain\ndev', description: 'Select  Branch', name: 'branch')}

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

        // stage('test') {  {uper vala build nu 6: "build": "npm run build",}
        //     steps {
        //         sh 'npm run test'
        //     }
        // } "test": "npm run test",

        // stage('start') {
        //     steps {
        //         sh 'npm run start'
        //     } "start": "npm run start",
        // }
        stage('deploy') {
            environment {
                NETLIFY_AUTH_TOKEN = credentials('NETLIFY_AUTH_TOKEN')
                NETLIFY_SITE_ID = credentials('NETLIFY_SITE_ID')
            }
            
            steps {
                sh 'npm install netlify-cli'
                sh 'npx netlify deploy --site $NETLIFY_SITE_ID --auth $NETLIFY_AUTH_TOKEN --dir build/ --prod'
                echo 'this is master branch'
            }
        }
    }

}
