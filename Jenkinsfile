node {
  stage('init') {
    checkout scm
  }
  
  stage('build') {
    sh 'mvn clean package'
  }
  	
  stage('deploy') {
    def webAppName = 'TESTEWEBAPPJENKINS'
    def resourceGroup = 'RG_DEV_PHP' 
	def plan = 'SPFREE'
        // login Azure
    withCredentials([azureServicePrincipal('azsrvprincipal')]) {
      sh '''
        az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID
        az account set -s $AZURE_SUBSCRIPTION_ID
	      '''
    }
	
	 // Create WebAPp
	 
	 sh ''' az webapp create --name $webAppName --resource-group  $resourceGroup --plan $plan '''
	sh 'az logout'
  }
}



