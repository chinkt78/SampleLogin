def err = null
try {
  
    node {
      
        stage('Preparation') { 
            git credentialsId: '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', url: 'https://github.com/chinkt78/SampleLogin.git'
        }
      
        stage('Dependencies') {
                sh 'export JAVA_HOME=/Users/chin/Library/Java/JavaVirtualMachines/corretto-1.8.0_292/Contents/Home'
                sh 'export ANDROID_HOME=/Users/chin/Library/Android/sdk'
                sh 'echo $JAVA_HOME'
        }
        
        stage('Clean Build') {
                dir("android") {
                    sh "pwd"
                    sh 'ls -al'
                    sh './gradlew clean'
                }   
        }
        
        stage('Build release ') {
            parameters {
                credentials credentialType: 'org.jenkinsci.plugins.plaincredentials.impl.FileCredentialsImpl', defaultValue: '9b7ea548-84bf-4b81-9fd2-8b8faef63a95', description: '', name: 'keystore', required: true
            }
            dir("android") {
                sh './gradlew assembleRelease'
            }
        }
      
        stage('Compile') {
            archiveArtifacts artifacts: '**/*.apk', fingerprint: true, onlyIfSuccessful: true            
        }
    }
  
} catch (caughtError) { 
    
    err = caughtError
    currentBuild.result = "FAILURE"

} finally {
    
    if(currentBuild.result == "FAILURE"){
              sh "echo 'Build FAILURE'"
    }else{
         sh "echo 'Build SUCCESSFUL'"
    }
   
}
