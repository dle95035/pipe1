
@Library('Utilities@1.5')  
import static org.conf.Utilities.* 

node ('node1'){
	stage ('source') {
		git 'https://github.com/dle95035/hello.git'
	}
	
	stage ('build') {
		 gbuild this, 'clean build'
	}
}