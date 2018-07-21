
@Library('Utilities@master')  
import static org.conf.Utilities.* 
import jenkins.model.*

node ('node1'){

	try {
		stage ('source') {
			git 'https://github.com/dle95035/hello.git'
		}
		
		stage ('build') {
			// gbuild this, 'clean build'
			// execute required unit tests in parallel
			parallel ( 
			worker2: { node ('worker_node2'){ 
				// always run with a new workspace 
				sleep 20 
			}}, 
			worker_s1: { node ('worker_slave_1'){ 
				// always run with a new workspace 
				sleep 10
				pwd
				echo hello
			}}, 
       )   
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