// pipeline
// {
//   agent any
  
//   tools
//   {
//     maven 'Maven_3.8.2'
//   }
  
//   triggers
//   {
//     pollSCM('* * * * *')
//   }
  
//   options
//   {
//     timestamps()
//     buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5'))
//   }
  
//   stages
//   {
//     stage('Checkout Code from GitHub')
//     {
//       steps()
//       {
//         git branch: 'development', credentialsId: '957b543e-6f77-4cef-9aec-82e9b0230975', url: 'https://github.com/devopstrainingblr/maven-web-application-1.git'
//       }
//     }
    
//     stage('Build Project')
//     {
//       steps()
//       {
//         sh "mvn clean package"
//       }
//     }
    
//     stage('Execute SonarQube Report')
//     {
//       steps()
//       {
//         sh "mvn clean sonar:sonar"
//       }
//     }
    
//     stage('Upload Artifacts to Sonatype Nexus')
//     {
//       steps()
//       {
//         sh "mvn clean deploy"
//       }
//     }
    
//     stage('Deploy Application to Tomcat')
//     {
//       steps()
//       {
//         sshagent(['bfe1b3c1-c29b-4a4d-b97a-c068b7748cd0'])
//         {
//           sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@35.154.190.162:/opt/apache-tomcat-9.0.50/webapps/"
//         }
//       }
//     }
//   }

// post
// {
//   success
//   {
//     emailext to: 'devopstrainingblr@gmail.com,mithuntechnologies@yahoo.com',
//     subject: "Pipeline Build is Over Build # is ${env.BUILD_NUMBER} and Build Status is ${currentBuild.result}",
//     body: "Pipeline Build is Over Build # is ${env.BUILD_NUMBER} and Build Status is ${currentBuild.result}",
//     replyTo: 'devopstrainingblr@gmail.com'
//   }
//   failure
//   {
//     emailext to: 'devopstrainingblr@gmail.com,mithuntechnologies@yahoo.com',
//     subject: "Pipeline Build is Over Build # is ${env.BUILD_NUMBER} and Build Status is ${currentBuild.result}",
//     body: "Pipeline Build is Over Build # is ${env.BUILD_NUMBER} and Build Status is ${currentBuild.result}",
//     replyTo: 'devopstrainingblr@gmail.com'
//     }
//   }
// }




// node {
//     // Defines the path to the Maven installation
//     def mavenHome = tool name: 'maven-3.8.2'
    
//     stage('Checkout Stage') {
//         git credentialsId: '3cd41dc2-c48d-4843-a2f6-58661f5c2121', 
//             url: 'https://github.com/bhargavM18/maven-web-application.git'
//     }
    
//     stage('Build') {
//         // Added the '$' before the curly braces
//         sh "${mavenHome}/bin/mvn clean package"
//     }
//      stage('SonarQ Test') {
//         // Added the '$' before the curly braces
//         sh "${mavenHome}/bin/mvn clean package sonar:sonar"
//     }
//     stage('Deploy War Into Container'){
//      sshagent(['a1e3132a-48ca-4722-bb22-ad3f22e2f7cc']) {
//     sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@ec2-13-201-48-218.ap-south-1.compute.amazonaws.com:/opt/tomcat/webapps/amazon-app.war"

//   }
        
//     }



node {
    // Defines the path to the Maven installation
    def mavenHome = tool name: 'maven-3.8.2'
    
    stage('Checkout Stage') {
        git credentialsId: '3cd41dc2-c48d-4843-a2f6-58661f5c2121', 
            url: 'https://github.com/bhargavM18/maven-web-application.git'
    }
    
    stage('Build') {
        sh "${mavenHome}/bin/mvn clean package"
    }

    stage('SonarQ Test') {
        // Ikkada 'env.BRANCH_NAME' vaadithe, SonarQube lo separate projects create avthayi
        // Example: facebook-master, facebook-uat, facebook-dev
        sh "${mavenHome}/bin/mvn sonar:sonar -Dsonar.projectKey=facebook-${env.BRANCH_NAME} -Dsonar.projectName=Facebook-App-${env.BRANCH_NAME}"
    }

    stage('Deploy War Into Container'){
        sshagent(['a1e3132a-48ca-4722-bb22-ad3f22e2f7cc']) {
            // Target file ni dynamic ga deploy chestundi
            sh "scp -o StrictHostKeyChecking=no target/*.war ec2-user@ec2-13-201-48-218.ap-south-1.compute.amazonaws.com:/opt/tomcat/webapps/amazon-app.war"
        }
    }
}
    
    
    
// }
