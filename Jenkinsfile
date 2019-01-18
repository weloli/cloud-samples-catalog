#!/usr/bin/env groovy

@Library('piper-lib-os') _

node() {
	stage('Prepare') {
		deleteDir()
		checkout scm
		setupCommonPipelineEnvironment script: this
	}

	stage('Build') {
		mtaBuild script: this, dockerImage: 'mta:latest', buildTarget: 'CF'
	}

	stage('Deploy') {
		cloudFoundryDeploy script: this, deployTool: 'mtaDeployPlugin', mtaPath: '*.mtar'
	}

	stage('Test') {
		newmanExecute script: this, newmanEnvironment: 'integration/ProductCatalog.postman_environment.json', failOnError: false
		testsPublishResults script: this, junit: [pattern: '**/newman/TEST-*.xml']
	}
}