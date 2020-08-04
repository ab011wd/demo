// Defining application parameters 
      def appName="demo-nonfuse"
      def git_repo="git@github.com:soumilajmera/demo.git"
      def branchName="master"
      def gitCredentialId="d25603e9-53c9-460b-be09-4f1195ecf93f"
      
// Template for  maven slave with mvn-3.6.3 and java 11 image 
podTemplate(label: "$appName-pod", 
             cloud: "openshift", 
             inheritFrom: "maven",
             containers: [
                containerTemplate(name: "jnlp", 
                       image: "docker-registry.default.svc:5000/amol-devops/jenkins-maven-agent-custom-jdk11-mvn3.6.3:test1", 
                       resourceRequestMemory: "512Mi", 
                       resourceLimitMemory: "1024Mi", 
                       envVars: [
                envVar(key: "CONTAINER_HEAP_PERCENT", value: "0.25"),
    ])
]){

//starting agent node 
  node("$appName-pod") {
  
//git checkout on slave node              
            stage("Checkout") {
            
   			                                
			               git branch: "$branchName" , credentialsId: "$gitCredentialId", url: "$git_repo"
                           //checkout changelog: false, poll: false, scm: [$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'd25603e9-53c9-460b-be09-4f1195ecf93f', url: 'ssh://git@bitbucket-agl.absa.co.za:7999/~ab0120w/devops.git']]]
                        }
            stage("Test"){
                sh "ls"
            }
                }
          
}
         
