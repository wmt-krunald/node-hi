pipeline {
    agent any
    
    tools {nodejs "node"}

    environment {
        CI = 'true'
    }

    // parameters{
    //     choice(choices:'master\nmain\ndev', description: 'Select  Branch', name: 'branch')
    //     choice(choices:'chrome\nfirefox', description: 'Select Browser', name: 'browser')
    //     choice(choices:'https://snapshott.netlify.app\nhttps://qa.snapshott.netlify.app\nhttps://qa1.snapshott.netlify.app', description: 'Select URL.', name: 'url')
    // }

    stages {

        stage('branch-check') {
            steps {
                sh 'git branch'
                sh 'git checkout $branch'
            }
        }

        stage('check') {
            steps {
            sh 'npm config ls'
            }
        }

        stage('build') {
            steps {
                sh 'npm i'
            }
        }

        // stage('test') {
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
