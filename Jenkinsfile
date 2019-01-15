#!/usr/bin/env groovy

@Library('piper-lib-os') _

node() {
	stage('Clone') {
		deleteDir()
		checkout scm
		setupCommonPipelineEnvironment script: this
	}

	stage('Build') {
		mtaBuild script: this, dockerImage: 'mta:latest', buildTarget: 'CF'
	}

	stage('Deploy') {
		cloudFoundryDeploy script: this, deployTool: 'mtaDeployPlugin'
	}
}