pipeline {
    agent {
	  label 'master'
        }

	triggers {
           pollSCM('* * * * *')
	}

	environment {
		ANSIBLE_CONFIG = "Jenkins-LTS/ansible.cfg"
		}
        stages{
	    stage('Checkout') {
		steps {
                   checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'RelativeTargetDirectory', relativeTargetDir: 'Jenkins-LTS'], [$class: 'WipeWorkspace']], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'fd864bf0-5e33-4cf1-a130-67ac2c22bf17', url: 'https://github.com/MRDO5/jenkins-lts.git']]])
 			}
		}
			stage('Syntax check') {
				steps {
				      ansiblePlaybook become: true, 
				      colorized: true,
				      credentialsId: '7980492c-7fa3-41b6-9c8e-b44d3f7ce236',
				      extras: '--syntax-check' ,
			              inventory: 'Jenkins-LTS/inventory',
				      playbook: 'Jenkins-LTS/main.yml'
					} 
				    }
				
			 stage('Check provision for virtual machines') {
				 steps {
				   ansiColor('xterm') {
				      ansiblePlaybook become: true, 
				      colorized: true,
				      credentialsId: '7980492c-7fa3-41b6-9c8e-b44d3f7ce236',
				      installation: 'ansible',
				      inventory: 'Jenkins-LTS/inventory',
				      playbook: 'Jenkins-LTS/main.yml'
				   }
 	                     }
                       }
               }
      }

