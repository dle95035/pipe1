
node ('node1'){
    def gradleHome
	gradleHome = tool 'gradle32'
	stage ('source') {
		git 'https://github.com/dle95035/hello.git'
	}
	
	stage ('build-node1') {
		sh  "'${gradleHome}/bin/gradle' clean build" 
	}
}