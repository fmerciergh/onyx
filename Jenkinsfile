node {
    
	agent { label 'CIT-WIN10' }

    				
	stage('Init') {
    	
		bat 'if exist C:\\LINUX\\setup rd /q /s C:\\LINUX\\setup'
		bat 'if exist C:\\LINUX\\unittest rd /q /s C:\\LINUX\\unittest'
		bat 'mkdir C:\\LINUX\\setup'
		bat 'mkdir C:\\LINUX\\unittest'
		
		// checkout scripts CIT + checkout TESTS
	}
		
    stage('Build') {
    	bat 'docker run -v C:\\LINUX\\setup:/home/setup -v C:\\LINUX\\unittest:/home/unittest mapping/buildlinux_trunk'
    }
    
    stage('Unit Test') {
    }
    
    stage('Integration Test') {
		
		
		// Creation image pour les tests : linuxtestbase + install setup.tar.gz
		//sshCommand remote: remote, command: "svn checkout -q --non-interactive --username exploit --password VsS3o2s8 svn://192.168.216.21/mappingsuite/M-Suite/trunk/ContinuousIntegration/linux/tests C:\\LINUX\\tests"
		//sshCommand remote: remote, command: "svn checkout -q --non-interactive --username exploit --password VsS3o2s8 svn://192.168.216.21/CIT/mapping/Onyx C:\\LINUX\\tests\\cases"
		
		bat 'copy /Y C:\\LINUX\\setup\\* C:\\LINUX\\tests\\image\\setup\\'
		bat 'cd C:\\LINUX\\tests\\scripts && javac executeTest.java && javac mdesigner.java'
		
		// generation maquette
		bat 'cd C:\\LINUX\\tests\\scripts && generateMDesigner.bat "C:\\LINUX\\tests\\cases"'
		
		bat 'cd C:\\LINUX\\tests\\image && docker-compose up'
		
	
		
		// Launch script qui run l'image pour chaque case
    }
	
	stage('Changelog') {
    }
    
    stage('Deploy') {
    }
	
	stage('Clean') {
	
	 // suppression de tout
    }
	
}