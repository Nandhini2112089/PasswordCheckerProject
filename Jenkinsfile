pipeline {
    agent any

    environment {
        VENV_PATH = "${WORKSPACE}/venv/bin"
        PATH = "${VENV_PATH}:${env.PATH}"
    }

    stages {
        stage('Setup Virtualenv & Install Dependencies') {
            steps {
                sh '''
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install pyinstaller fastapi uvicorn pydantic
                '''
            }
        }

        stage('Build Package') {
            steps {
                sh '''
                    . venv/bin/activate
                    pyinstaller -y password_checker/main.py --distpath bin --name password_checker --paths password_checker/app
                '''
            }
        }

        stage('Archive') {
            steps {
                println "check here"
                println Test
                archiveArtifacts artifacts: 'bin/**/*', allowEmptyArchive: true

            }
        }
    }

}
