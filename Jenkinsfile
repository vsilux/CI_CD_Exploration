#!/usr/bin/env groovy
pipeline {
    agent any
    parameters {
        string(name: 'BUILD_NUMBER', defaultValue: '', description: 'Номер збірки у TestFlight')
    	string(name: 'VERSION', defaultValue: '', description: 'Версия збірки у TestFlight')
    }
    stages {
        stage('Pre-Build') {
            steps {
                sh """
            	agvtool new-version -all ${params.BUILD_NUMBER}
            	agvtool new-marketing-version ${params.VERSION}
            	echo n
               """
            }
        }
        stage('Build') {
            steps {
                sh '''
                    xcodebuild -workspace CI_CD_Exploration.xcodeproj/project.xcworkspace -scheme CI_CD_Exploration -destination 'platform=iOS Simulator,name=Any iOS Simulator Device' -derivedDataPath Build/ -configuration Debug
                '''
            }
        }
    }
}