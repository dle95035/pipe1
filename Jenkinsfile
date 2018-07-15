
@Library('Utilities@master')  
import static org.conf.Utilities.* 

node ('node1'){

	try {
		stage ('source') {
			git 'https://github.com/dle95035/hello.git'
		}
		
		stage ('build') {
			gbuild this, 'clean build'
		}
		
		stage ('verify') {
			def verifyCall = load("/root/shared-libraries/src/verify.groovy") 
			timeout(time: 5, unit: 'SECONDS') {
				verifyCall("Please Verify the build")
			}
			
		}
	}
	catch (err) {
		 echo "Caught: ${err}" 
	}
	stage ('Notify') {
		echo "here is my last step!"
	}
	
} 