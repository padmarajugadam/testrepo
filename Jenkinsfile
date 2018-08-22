pipeline {
	
stages {
	agent { label 'windows'}
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
    bat 'jar xf scm-server-1.60-app.zip'

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
    bat  '''del C:\\flx\\bin'
	xcopy C:\\staging\\scm-server-1.60-app\\scm-server\\bin F:\\fix\\
	set year=%datetime:~0,4%
    set month=%datetime:~4,2%
    set day=%datetime:~6,2%
	rename F:\\fix\\scm-server.bat F:\\fix\\scm-server_%year%%month%%day%.bat
'''
}

}
stage('restart') { 
            steps {
                //restart the pc  
    bat  'shutdown /r /f '
}

}

}
}
