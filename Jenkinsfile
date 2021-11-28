def imageName = 'skyglass/movies-loader'
node('workers'){
    stage('Checkout'){
        checkout scm
    }

    stage('Unit Tests'){
        def imageTest= docker.build("${imageName}-test", "-f Dockerfile.test .")
        sh "docker run --rm -v $PWD/reports-new:/app/reports ${imageName}-test"
        sh "ls $PWD/reports-new"
        junit 'reports-new/TEST-TestJSONLoaderMethods-20211128172121.xml'
    }
}

def commitID() {
    sh 'git rev-parse HEAD > .git/commitID'
    def commitID = readFile('.git/commitID').trim()
    sh 'rm .git/commitID'
    commitID
}