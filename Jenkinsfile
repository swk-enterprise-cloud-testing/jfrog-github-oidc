pipeline {
    agent any
    tools {
        jfrog 'jfrog-cli',
        node 'nodejs'
    }
    stages {
        stage('Clone') {
            steps {
                git branch: 'master', url: "https://github.com/jfrog/project-examples.git"
            }
        }

        stage('Exec npm commands') {
            steps {
                dir('npm-example') {
                    // Configure npm project's repositories
                    jf 'npm-config --repo-resolve my-npm --repo-deploy my-npm'

                    // Install dependencies
                    jf 'npm install'

                    // Pack and deploy the npm package
                    jf 'npm publish'
                }
            }
        }

        stage('Publish build info') {
            steps {
                jf 'rt build-publish'
            }
        }
    }
}