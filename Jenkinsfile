
@Library('Utilities@master')  
import static org.conf.Utilities.* 
import jenkins.model.*
jenkins = Jenkins.instance

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
			worker3: { node ('worker_slave_1'){ 
				// always run with a new workspace 
				bash /root/test.sh
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