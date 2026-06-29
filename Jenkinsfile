// =============================================================
// RVCE Todo App - Jenkins Declarative Pipeline (Windows)
// =============================================================

pipeline {

    agent any

    stages {

        // ---------------------------------------------------------
        // Stage 1 : Checkout
        // ---------------------------------------------------------
        stage('Checkout') {

            steps {

                echo 'Checking out source code...'

                checkout scm

                bat '''
                @echo off

                echo =====================================
                echo Repository Information
                echo =====================================

                echo.
                echo Current Directory:
                cd

                echo.
                echo Git Version:
                git --version

                echo.
                echo Current Branch:
                git branch --show-current

                echo.
                echo Latest Commit:
                git rev-parse HEAD

                echo.
                dir
                '''
            }
        }

        // ---------------------------------------------------------
        // Stage 2 : Verify Repository Structure
        // ---------------------------------------------------------
        stage('Verify Project Structure') {

            steps {

                bat '''
                @echo off

                echo =====================================
                echo Verifying Repository Structure
                echo =====================================

                if not exist client (
                    echo ERROR: client folder missing
                    exit /b 1
                )

                if not exist server (
                    echo ERROR: server folder missing
                    exit /b 1
                )

                if not exist package.json (
                    echo ERROR: package.json missing
                    exit /b 1
                )

                if not exist Dockerfile (
                    echo ERROR: Dockerfile missing
                    exit /b 1
                )

                if not exist docker-compose.yml (
                    echo ERROR: docker-compose.yml missing
                    exit /b 1
                )

                if not exist README.md (
                    echo ERROR: README.md missing
                    exit /b 1
                )

                if not exist Jenkinsfile (
                    echo ERROR: Jenkinsfile missing
                    exit /b 1
                )

                echo.
                echo Repository verification successful.
                '''
            }
        }

        // ---------------------------------------------------------
        // Stage 3 : Install Root Dependencies
        // ---------------------------------------------------------
        stage('Install Root Dependencies') {

            steps {

                echo 'Installing root dependencies...'

                bat 'npm install'
            }
        }

        // ---------------------------------------------------------
        // Stage 4 : Install Server Dependencies
        // ---------------------------------------------------------
        stage('Install Server Dependencies') {

            steps {

                dir('server') {

                    bat 'npm install'

                }

            }

        }

        // ---------------------------------------------------------
        // Stage 5 : Install Client Dependencies
        // ---------------------------------------------------------
        stage('Install Client Dependencies') {

            steps {

                dir('client') {

                    bat 'npm install'

                }

            }

        }

        // ---------------------------------------------------------
        // Stage 6 : Verify Environment
        // ---------------------------------------------------------
        stage('Verify Environment') {

            steps {

                bat '''
                @echo off

                echo =====================================
                echo Environment Information
                echo =====================================

                echo.
                echo Node Version
                node -v

                echo.
                echo NPM Version
                npm -v

                echo.
                echo Git Version
                git --version

                echo.
                echo Docker Version
                docker --version

                echo.
                echo =====================================
                '''
            }

        }

        // ---------------------------------------------------------
        // Stage 7 : Success
        // ---------------------------------------------------------
        stage('Pipeline Complete') {

            steps {

                echo '''
========================================================

BUILD SUCCESSFUL

Repository Checked Out

Repository Structure Verified

Dependencies Installed

Environment Verified

Project Ready For Docker Deployment

========================================================
'''

            }

        }

    }

    post {

        success {

            echo 'Pipeline completed successfully.'

        }

        failure {

            echo 'Pipeline failed.'

        }

        always {

            echo 'Build Finished.'

        }

    }

}
