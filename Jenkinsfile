pipeline {
	agent any

  stages {
	  stage('Building and gtesting'){
		  agent { label('windows || linux') }
		  
		  steps{
	    
	cmakeBuild buildDir: 'build', installation: 'InSearchPath', steps: [[withCmake: true]]
	
		   }  }
	  stage('Cppcheck'){
		  agent { label('windows || linux') }
		  steps{
			  script{
			   if (isUnix()) {
    				sh "cppcheck  --xml --xml-version=2 . 2> cppcheck.xml"
} else {
			  bat "cppcheck  --xml --xml-version=2 . 2> cppcheck.xml"
			   }}
			  publishCppcheck allowNoReport: true, pattern: '**/cppcheck.xml'
		  }}
	  
  	stage('gtest'){
		agent { label('windows || linux') }
		  steps{
			  script{
			  if (isUnix()) {
				  sh "cd /var/lib/jenkins/workspace/cmaketestl1/build/test && ./mytest --gtest_output=xml:testresults.xml"
			  }
				  else{
			  bat "cd build/test/debug && mytest --gtest_output=xml:testresults.xml"
				  }}
		  }}
  }}

