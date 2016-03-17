node('jdk7') {

	stage 'build'
		echo "build"

	stage 'integration-test'
		echo "integration"
}

stage 'quality-and-functional-test'

	parallel(qualityTest: {
    	node('jdk7') {
    		echo 'sonar scan'
        	// sh 'mvn sonar:sonar'
    	}
    }, functionalTest: {
    	echo 'selenium test'
        // build 'sauce-labs-test'
    })

    try {
        checkpoint('Testing Complete')
    } catch (NoSuchMethodError _) {
        echo 'Checkpoint feature available in Jenkins Enterprise by CloudBees.'
    }


stage 'approval'
	input 'Do you approve deployment to production?'

stage 'production'
	echo 'mvn cargo:deploy'
