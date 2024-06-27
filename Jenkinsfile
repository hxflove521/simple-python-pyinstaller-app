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
                	sh '/home/he/.pyenv/shims/pytest --junit-xml test-reports/results.xml sources/test_calc.py'
            	    }
		}
            post {
                always {
                    junit 'test-reports/results.xml'
                }
            }
        }
    }
}
