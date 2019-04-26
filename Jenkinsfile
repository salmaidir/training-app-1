node {
   def mvnHome
   stage('Preparation') { // for display purposes
      // Get some code from a GitHub repository
      git 'https://github.com/salmaidir/training-app-1.git'
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'Maven3'
   }
   stage('Test') {
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' clean test"
      } else {
         bat(/"${mvnHome}\bin\mvn" clean test/)
      }
   }
      stage('Build') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Dmaven.test.failure.ignore clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" -B -DskipTests -Dmaven.test.failure.ignore package/)
      }
   }
   stage('Results') {
      junit '**/target/surefire-reports/TEST-*.xml'
      archiveArtifacts 'target/*.jar'
   }
   stage('Execute Jar') {
       if (isUnix()) {
           sh "java -jar target/*.jar"
       } else {
           bat(/java -jar target\/training-app-2.0-jar-with-dependencies.jar/)
       }
   }
    stage('publish Artefact') {
      
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' -Ddeployonly deploy"
      } else {
         bat(/"${mvnHome}\bin\mvn" -Ddeployonly deploy -s "C:\apache-maven-3.6.0\conf\settings.xml"/)
      }
   }
}
