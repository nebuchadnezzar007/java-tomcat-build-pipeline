node{
      def mvnHome = tool name: 'maven 3.5.4', type: 'maven' 
      stage('Checkout'){
         echo "https://github.com/LovesCloud/java-tomcat-build-pipeline"
         git 'https://github.com/nebuchadnezzar007/java-tomcat-build-pipeline.git'
       
      }  
      stage('Build'){
         //// Get maven home path and build
        sh "${mvnHome}/bin/mvn clean package -Dmaven.test.skip=true"
      }
     stage ('Test-JUnit'){
         sh "'${mvnHome}/bin/mvn' test surefire-report:report"
      }  
    
      stage('Deploy') {     
          sshagent(['tomcatsshuser']) {
               sh 'scp -o StrictHostKeyChecking=no target/demojavapipeline_paulnewuser.war jenkins@35.193.54.220:/opt/tomcat/webapps'
              
          }
         
     }
      
 }
