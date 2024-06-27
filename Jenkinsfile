pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
		withPythonEnv('/home/he/.pyenv/versions/venv312/bin/python') {
                	sh 'python -m py_compile sources/add2vals.py sources/calc.py'
		} 
                stash(name: 'compiled-results', includes: 'sources/*.py*') 
            }
        }
	stage('Test') {
            steps {
		withPythonEnv('/home/he/.pyenv/versions/venv312/bin/python') {
                	sh 'py.test --junit-xml test-reports/results.xml sources/test_calc.py'
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
