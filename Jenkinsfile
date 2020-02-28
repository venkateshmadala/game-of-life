#!groovy?
node(){
    compile()
}

def compile(){
 stage('CleanUp') {
  cleanWs()
 }
    stage('Checkout') {
            checkout scm 
    }
    stage('Compile') {
            def pom_version = version()
            mvn "compile"  
    }
    stage('Test') {
            def pom_version = version()
            mvn "test"  
    }
    stage('Package') {
            def pom_version = version()
            mvn "package"  
    }
    stage('Nexus Upload'){
            curl -v -u admin:admin --upload-file target/gameoflife.war http://127.0.0.1:8081/repository/artifacts/demoproject/
    }
}

def mvn(String goals) {
    def mvnHome = tool "maven"
    withEnv(["PATH+MAVEN=${mvnHome}/bin"]) {
        sh "mvn ${goals}"
    }
}

def version() {
    pom = readMavenPom file: 'pom.xml'
    return pom.version
}
