
node {
   // This is to demo github action	
   
   def mvn = tool (name: 'maven-3', type: 'maven') + '/bin/mvn'
   stage('SCM Checkout'){
    // Clone repo
	git branch: 'master', 
	credentialsId: 'github', 
	url:'https://github.com/Smaheshwar85/Devops_basic_step'
   
   }
   stage('Mvn Package'){
	   // Build using maven
	   
	   sh "${mvn} clean package"
   }
   
   stage('deploy-dev'){
       def tomcatDevIp = '172.31.59.249'
	   def tomcatHome = '/opt/tomcat/'
	   def webApps = tomcatHome+'webapps/'
	   def tomcatStart = "${tomcatHome}bin/startup.sh"
	   def tomcatStop = "${tomcatHome}bin/shutdown.sh"
	   
	   sshagent (credentials: ['tomcat-dev']) {
	      sh "scp -o StrictHostKeyChecking=no target/myweb*.war ubuntu@${tomcatDevIp}:${webApps}/"
          sh "ssh ubuntu@${tomcatDevIp} ${tomcatStop}"
		  sh "ssh ubuntu@${tomcatDevIp} ${tomcatStart}"
       }
   }
   
}

