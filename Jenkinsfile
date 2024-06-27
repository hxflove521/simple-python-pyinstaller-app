pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh 'pyenv activate venv312 && python -m py_compile sources/add2vals.py sources/calc.py' 
                stash(name: 'compiled-results', includes: 'sources/*.py*') 
            }
        }
    }
}
