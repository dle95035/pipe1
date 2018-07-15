
@Library('Utilities@master')  
import static org.conf.Utilities.* 

node ('node1'){
	stage ('source') {
		git 'https://github.com/dle95035/hello.git'
	}
	
	stage ('build') {
		 gbuild this, 'clean build'
	}
	
	stage ('verify') {
		def verifyCall = load("/root/shared-libraries/src/verify.groovy") 
        verifyCall("Please Verify the build")
	}
} 