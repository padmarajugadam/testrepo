

pipeline {
	agent any
	node ('window-slave')
stages {
	
        stage('FTP') { 
		
            steps {
                //connecting to ftp and downloading 
    bat '''cd C:\\staging
echo open > scriptfile.txt
echo 172.31.30.218 >> scriptfile.txt
echo USER padmaraju chinna@123 >> scriptfile.txt
echo cd C:\\ftp-client >> scriptfile.txt
echo get scm-server-1.60-app.zip  >> scriptfile.txt
ftp -n -v -s:scriptfile.txt
'''

}

}
stage('Extract') { 
	
            steps {
                //extracting the binaries  
    bat '''cd C:\\staging
    "C:\\Program Files\\Java\\jdk1.8.0_181\\bin\\jar.exe" -xv scm-server-1.60-app.zip
    
    '''

}

}
stage('ServiceStop') { 
	
            steps {
                //stoping the service  
    bat 'echo net stop Calculator'

}

}
stage('copyBin64') { 
	
            steps {
                //extracting the binaries  
    bat  '''RD /S /Q C:\\flx\\bin
	xcopy C:\\staging\\scm-server\\bin C:\\flx\\bin /y /i /s
	for /f "tokens=2 delims==" %%G in ('wmic os get localdatetime /value') do set datetime=%%G
	set year=%datetime:~0,4%
    set month=%datetime:~4,2%
    set day=%datetime:~6,2%
	rename C:\\flx\\bin\\scm-server.bat scm-server_%year%%month%%day%.bat
'''
}

}
stage('restart') { 
	
            steps {
                //restart the pc  
    bat  'echo shutdown /r /f '
}

}

}
}
