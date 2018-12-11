node {
    
	def remote = [:]
	remote.name = 'CIT-WIN10'
	remote.host = 'CIT-WIN10'
	remote.user = 'CIT'
	remote.password = 'Mapping1234$'
	remote.allowAnyHosts = true

    				
	stage('Init') {
    	
		sshCommand remote: remote, command: "if exist C:\\LINUX\\setup rd /q /s C:\\LINUX\\setup"
		sshCommand remote: remote, command: "if exist C:\\LINUX\\unittest rd /q /s C:\\LINUX\\unittest"
		sshCommand remote: remote, command: "mkdir C:\\LINUX\\setup"
		sshCommand remote: remote, command: "mkdir C:\\LINUX\\unittest"
		
		// checkout scripts CIT + checkout TESTS
	}
	
	stage('Build Images') {
    	
		// TODO ne pas faire ça ici
		// sshCommand remote: remote, command: "cd C:\\LINUX\\BUILD && docker-compose up"
		// sshCommand remote: remote, command: "cd C:\\LINUX\\TEST\\BASE && docker-compose up"
    }
		
    stage('Build') {
    	sshCommand remote: remote, command: "docker run -v C:\\LINUX\\setup:/home/setup -v C:\\LINUX\\unittest:/home/unittest mapping/buildlinux_trunk"
    }
    
    stage('Unit Test') {
    }
    
    stage('Integration Test') {
		
		
		// Creation image pour les tests : linuxtestbase + install setup.tar.gz
		//sshCommand remote: remote, command: "svn checkout -q --non-interactive --username exploit --password VsS3o2s8 svn://192.168.216.21/mappingsuite/M-Suite/trunk/ContinuousIntegration/linux/tests C:\\LINUX\\tests"
		//sshCommand remote: remote, command: "svn checkout -q --non-interactive --username exploit --password VsS3o2s8 svn://192.168.216.21/CIT/mapping/Onyx C:\\LINUX\\tests\\cases"
		sshCommand remote: remote, command: "copy /Y C:\\LINUX\\setup\\* C:\\LINUX\\tests\\image\\setup\\"
		sshCommand remote: remote, command: "cd C:\\LINUX\\tests\\scripts && javac executeTest.java && javac mdesigner.java"
		
		// generation maquette
		sshCommand remote: remote, command: "cd C:\\LINUX\\tests\\scripts && generateMDesigner.bat 'C:\\LINUX\\tests\\cases'"
		
		sshCommand remote: remote, command: "cd C:\\LINUX\\tests\\image && docker-compose up"
		
	
		
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