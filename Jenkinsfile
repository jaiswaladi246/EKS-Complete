pipeline {
    agent any
    
    environment {
        
        SCANNER_HOME = tool 'sonar-scanner'
    }

    stages {
        stage('Git Checkout') {
            steps {
                git branch: 'latest', url: 'https://github.com/jaiswaladi246/10-Tier-MicroService-Appliction.git'
            }
        }
        
        stage('SonarQube') {
            steps {
                
                withSonarQubeEnv('sonar') {
                    sh ''' $SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=10-Tier -Dsonar.projectName=10-Tier -Dsonar.java.binaries=. '''
                }
               
            }
        }
        
        stage('adservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/adservice/') {
                                 sh "docker build -t adijaiswal/adservice:latest ."
                                 sh "docker push adijaiswal/adservice:latest"
								 sh " docker rmi adijaiswal/adservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('cartservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/cartservice/src/') {
                                 sh "docker build -t adijaiswal/cartservice:latest ."
                                 sh "docker push adijaiswal/cartservice:latest"
								 sh " docker rmi adijaiswal/cartservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('checkoutservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/checkoutservice/') {
                                 sh "docker build -t adijaiswal/checkoutservice:latest ."
                                 sh "docker push adijaiswal/checkoutservice:latest"
								 sh " docker rmi adijaiswal/checkoutservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('currencyservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/currencyservice/') {
                                 sh "docker build -t adijaiswal/currencyservice:latest ."
                                 sh "docker push adijaiswal/currencyservice:latest"
								 sh " docker rmi adijaiswal/currencyservice:latest"
                        }
                    }
                }
            }
        }
        
		stage('emailservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/emailservice/') {
                                 sh "docker build -t adijaiswal/emailservice:latest ."
                                 sh "docker push adijaiswal/emailservice:latest"
								 sh " docker rmi adijaiswal/emailservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('frontend') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/frontend/') {
                                 sh "docker build -t adijaiswal/frontend:latest ."
                                 sh "docker push adijaiswal/frontend:latest"
								 sh " docker rmi adijaiswal/frontend:latest"
                        }
                    }
                }
            }
        }
		
		stage('loadgenerator') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/loadgenerator/') {
                                 sh "docker build -t adijaiswal/loadgenerator:latest ."
                                 sh "docker push adijaiswal/loadgenerator:latest"
								 sh " docker rmi adijaiswal/loadgenerator:latest"
                        }
                    }
                }
            }
        }
		
		stage('paymentservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/paymentservice/') {
                                 sh "docker build -t adijaiswal/paymentservice:latest ."
                                 sh "docker push adijaiswal/paymentservice:latest"
								  sh " docker rmi adijaiswal/paymentservice:latest"
                        }
                    }
                }
            }
        }
        
		stage('productcatalogservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/productcatalogservice/') {
                                 sh "docker build -t adijaiswal/productcatalogservice:latest ."
                                 sh "docker push adijaiswal/productcatalogservice:latest"
								 sh " docker rmi adijaiswal/productcatalogservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('recommendationservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/recommendationservice/') {
                                 sh "docker build -t adijaiswal/recommendationservice:latest ."
                                 sh "docker push adijaiswal/recommendationservice:latest"
								 sh " docker rmi adijaiswal/recommendationservice:latest"
                        }
                    }
                }
            }
        }
		
		stage('shippingservice') {
            steps {
                script{
                    withDockerRegistry(credentialsId: 'docker-cred', toolName: 'docker') {
                          dir('/var/lib/jenkins/workspace/10-Tier/src/shippingservice/') {
                                 sh "docker build -t adijaiswal/shippingservice:latest ."
                                 sh "docker push adijaiswal/shippingservice:latest"
								 sh " docker rmi adijaiswal/shippingservice:latest"
                        }
                    }
                }
            }
        }
        
        
        	stage('K8-Deploy') {
            steps {
                withKubeConfig(caCertificate: '', clusterName: 'my-eks8', contextName: '', credentialsId: 'k8-token', namespace: 'webapps', restrictKubeConfigAccess: false, serverUrl: 'https://2BCD568E04EC6456125F85067AFE81B9.gr7.ap-south-1.eks.amazonaws.com') {
                         sh 'kubectl apply -f deployment-service.yml'
                         sh 'kubectl get pods '
                         sh 'kubectl get svc'
                }
            }
        }
        
    }
}
