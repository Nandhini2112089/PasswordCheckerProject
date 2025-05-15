pipeline {
    agent any

    environment {
        VENV_PATH = "${WORKSPACE}/venv/bin"
        PATH = "${VENV_PATH}:${env.PATH}"
        DEST_PATH = "${WORKSPACE}/artifact_output"
    }

    stages {
        stage("Setup Virtualenv & Install Dependencies") {
            steps {
                sh """
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install --upgrade pip
                    pip install pyinstaller fastapi uvicorn pydantic
                """
            }
        }

        stage("Build Package") {
            steps {
                sh """
                    . venv/bin/activate
                    pyinstaller -y password_checker/main.py --distpath bin --name password_checker --paths password_checker/app
                """
            }
        }

        stage("Zip Build") {
            steps {
                sh """
                    mkdir -p ${DEST_PATH}
                    zip -r ${DEST_PATH}/password_checker.zip bin/password_checker
                """
            }
        }

        stage("Archive") {
            steps {
                archiveArtifacts artifacts: "${DEST_PATH}/password_checker.zip", allowEmptyArchive: true
            }
        }
    }
}
