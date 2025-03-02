pipeline {
    agent any
    parameters {
        string(name: 'GIT_BRANCH', defaultValue: 'master', description: 'Selecciona la rama a compilar')
    }
    tools {
        maven 'Maven-3.9.6'
    }
    environment {
        GIT_REPO = 'https://github.com/jenkins-docs/simple-java-maven-app.git'
        WORKSPACE_DIR = "${WORKSPACE}/simple-java-maven-app"
    }
    stages {
        stage('Verificar y Eliminar Carpeta') {
            steps {
                script {
                    if (fileExists("${WORKSPACE_DIR}")) {
                        echo "🔴 Carpeta encontrada, eliminando..."
                        sh "rm -rf ${WORKSPACE_DIR}"
                    } else {
                        echo "✅ No se encontró carpeta previa."
                    }
                }
            }
        }
        stage('Clonar Código') {
            steps {
                echo "🌍 Clonando la rama: ${params.GIT_BRANCH}"
                git branch: "${params.GIT_BRANCH}", url: "${GIT_REPO}"
            }
        }
        stage('Compilar con Maven') {
            steps {
                echo "🚀 Compilando el proyecto..."
                sh 'mvn clean package'
            }
        }
    }
}
