pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh 'source /home/he/.pyenv/versions/venv312/bin/activate && python -m py_compile sources/add2vals.py sources/calc.py' 
                stash(name: 'compiled-results', includes: 'sources/*.py*') 
            }
        }
    }
}
