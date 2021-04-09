pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                script{
                    COMMIT_ID="${env.GIT_COMMIT}"
                    echo "${COMMIT_ID}"
                }
                echo "---------------------------------------------------"
                sh '''
                    git show --stat ${COMMIT_ID} 
                    '''
                echo "---------------------------------------------------"
            }
        }
        stage(' DEV Staging') {
		
		when {
  branch 'DEV'
}
            steps{
                script{
			sh '''
				rm -rf /ccwar/MIGRATION/DEV/DATABASE.txt
				rm -rf /ccwar/MIGRATION/DEV/DATABASE1.txt
				rm -rf /ccwar/MIGRATION/DEV/migration.txt
				rsync -rcvz /var/lib/jenkins/workspace/CIC_CDH_Demo_DEV/DATABASE/ /ccwar/CLAIMCENTER/DEV/DATABASE/ox5cd-scan/cdhdev.farmersinsurance.com/ | head --lines=-2 | tail --lines=+2 | grep -E -v \'/$\' > /ccwar/MIGRATION/DEV/migration.txt  
				grep -e \'.sql\' -e \'.SQL\' /ccwar/MIGRATION/DEV/migration.txt >> /ccwar/MIGRATION/DEV/DATABASE1.txt
				sed -i -e "/.sql\\|.SQL/d" /ccwar/MIGRATION/DEV/migration.txt
				awk \'{print "/ccwar/CLAIMCENTER/DEV/DATABASE/ox5cd-scan/cdhdev.farmersinsurance.com/"$0;}\' /ccwar/MIGRATION/DEV/DATABASE1.txt > /ccwar/MIGRATION/DEV/DATABASE.txt
				chmod -R 777 /ccwar/MIGRATION/DEV/DATABASE.txt
			'''
		}
	    }
	}
	stage(' SIT Staging') {
		
		when {
  branch 'SIT'
}
            steps{
                script{
			sh '''
				rm -rf /ccwar/MIGRATION/SIT/DATABASE.txt
				rm -rf /ccwar/MIGRATION/SIT/DATABASE1.txt
				rm -rf /ccwar/MIGRATION/SIT/migration.txt
				rm -rf /ccwar/MIGRATION/SIT/DATABASE.txt
				rsync -rcvz /var/lib/jenkins/workspace/CIC_CDH_Demo_SIT/DATABASE/ /ccwar/CLAIMCENTER/SIT/DATABASE/ok5cd-scan/cdhsir.farmersinsurance.com/ | head --lines=-2 | tail --lines=+2 | grep -E -v \'/$\' > /ccwar/MIGRATION/SIT/migration.txt  
				grep -e \'.sql\' -e \'.SQL\' /ccwar/MIGRATION/SIT/migration.txt >> /ccwar/MIGRATION/SIT/DATABASE1.txt
				sed -i -e "/.sql\\|.SQL/d" /ccwar/MIGRATION/SIT/migration.txt
				awk \'{print "/ccwar/CLAIMCENTER/SIT/DATABASE/ox5cd-scan/cdhsit.farmersinsurance.com/"$0;}\' /ccwar/MIGRATION/SIT/DATABASE1.txt > /ccwar/MIGRATION/SIT/DATABASE.txt
				chmod -R 777 /ccwar/MIGRATION/SIT/DATABASE.txt
			'''
		}
	    }
	}
	stage(' UAT Staging') {
		
		when {
  branch 'UAT'
}
            steps{
                script{
			sh '''
				rm -rf /ccwar/MIGRATION/UAT/DATABASE.txt
				rm -rf /ccwar/MIGRATION/UAT/DATABASE1.txt
				rm -rf /ccwar/MIGRATION/UAT/migration.txt
				rsync -rcvz /var/lib/jenkins/workspace/CIC_CDH_Demo_UAT/DATABASE/ /ccwar/CLAIMCENTER/UAT/DATABASE/ok5cd-scan/cdhuat.farmersinsurance.com/ | head --lines=-2 | tail --lines=+2 | grep -E -v \'/$\' > /ccwar/MIGRATION/UAT/migration.txt  
				grep -e \'.sql\' -e \'.SQL\' /ccwar/MIGRATION/UAT/migration.txt >> /ccwar/MIGRATION/UAT/DATABASE1.txt
				sed -i -e "/.sql\\|.SQL/d" /ccwar/MIGRATION/UAT/migration.txt
				awk \'{print "/ccwar/CLAIMCENTER/UAT/DATABASE/ox5cd-scan/cdhsit.farmersinsurance.com/"$0;}\' /ccwar/MIGRATION/UAT/DATABASE1.txt > /ccwar/MIGRATION/UAT/DATABASE.txt
				chmod -R 777 /ccwar/MIGRATION/UAT/DATABASE.txt
			'''
		}
	    }
	}
    }
}
