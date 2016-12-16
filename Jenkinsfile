node {
   def mvnHome
   
   stage('PilotApp') { // for display purposes
      // Get some code from a GitHub repository
     checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '944ecb3c-6812-4261-a03f-ac5839f04e7a', url: 'https://github.com/chandrayarramreddy/PilotProject.git']]])
      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
      mvnHome = tool 'M2_HOME'
   }
   stage('BuildPilotApp') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn' clean package"
      } else {
         bat(/"${mvnHome}\bin\mvn" clean package/)
      }
   stash includes: '**/*.war', name: 'PilotProject-0'

   }
  stage('TurnipApp') { // for display purposes
      // Get some code from a GitHub repository
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '944ecb3c-6812-4261-a03f-ac5839f04e7a', url: 'https://github.com/chandrayarramreddy/TurnipService.git']]])

      // Get the Maven tool.
      // ** NOTE: This 'M3' Maven tool must be configured
      // **       in the global configuration.           
  mvnHome = tool 'M2_HOME'
   }
   stage('BuildTurnip') {
      // Run the maven build
      if (isUnix()) {
         sh "'${mvnHome}/bin/mvn'  package"
      } else {
         bat(/"${mvnHome}\bin\mvn" package/)
      }
      unstash 'PilotProject-0'
   }
 //  build 'hello'
   
}
