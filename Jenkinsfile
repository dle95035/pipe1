
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
			worker1: { node ('linux-slave-1'){ 
				// always run with a new workspace 
				sleep 20 
				sh 'date >> /root/master.txt'
			}}, 
			worker2: { node ('linux-slave-1'){ 
				// always run with a new workspace 
				sleep 10
				sh 'echo the pipeline executed on slave 2'
				sh 'date >> /root/master.txt'
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