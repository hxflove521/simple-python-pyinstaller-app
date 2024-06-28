pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
		withPythonEnv('venv312') {
                	sh 'python -m py_compile sources/add2vals.py sources/calc.py'
		} 
                stash(name: 'compiled-results', includes: 'sources/*.py*') 
            }
        }
	stage('Test') {
            steps {
		withPythonEnv('venv312') {
                	sh 'python -m pytest sources/test_calc.py  --alluredir allure-results'
            	    }
		}
            post {
		 always {
                    allure includeProperties:
                     false,
                     jdk: '',
		     properties: [[key: '--name', value: ' GoogleAPI ']]
                     results: [[path: 'allure-results']]
                }
            }
        }
	 stage('Deliver') {
            steps {
		withPythonEnv('venv312') {
                	sh "pyinstaller --onefile sources/add2vals.py"
		}
            }
            post {
                success {
                    archiveArtifacts 'dist/add2vals'
                }
            }
        }
    }
}
