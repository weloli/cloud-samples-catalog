#!/usr/bin/env groovy

@Library('piper-lib-os') _

node() {
	stage('Clone') {
		deleteDir()
		checkout scm
		setupCommonPipelineEnvironment script: this
	}

	stage('Build') {
		mtaBuild script: this, dockerImage: 'node:8.14.0-alpine', mtaJarLocation: "${JENKINS_HOME}/userContent/mta.jar", buildTarget: 'CF'
	}
}