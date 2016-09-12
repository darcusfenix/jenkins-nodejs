node {
  stage ('Clonacion-de-proyecto'){
    git branch: 'master', 
        url: 'https://github.com/darcusfenix/jenkins-nodejs'
  }
  
  stage ("Actualizando dependencias"){
    //sh "npm update --save-dev"
    sh "echo 'HOLA'"
  }
}


node("aws-local"){
    sh "ls"
}


stage ("browser testing"){
    
    
    parallel chrome: {
        runTests("chrome")
    }, safari: {
        runTests("safari")
        
    }, firefox: {
        runTests("firefox")
    }
}

def runTests(browser){
        node("aws-local"){
            sh "ls"
        }
    }

node {
    notify("deploy to staging ?")    
}

input "Deploy to staging ?"


stage name: "Deploy", concurrency: 1

node {
    sh "echo '<h1>${env.BUILD_DISPLAY_NAME}</h1>' >> app7index-html"
    sh "docker ps"
    notify("deployed!")
}


def notify(status){
    emailext (
      to: "juancvfenix@gmail.com",
      subject: "${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
      body: """<p>${status}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at <a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a></p>""",
    )
}
