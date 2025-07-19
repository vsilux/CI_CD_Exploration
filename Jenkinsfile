#!/usr/bin/env groovy
pipeline {
    agent any
    parameters {
        string(name: 'BUILD_NUMBER', defaultValue: '', description: 'Номер збірки у TestFlight')
    	string(name: 'VERSION', defaultValue: '', description: 'Версия збірки у TestFlight')
    }
    stages {
        stage('Install Dependencies') {
            steps {
                sh '''
                    xcodegen generate
                    brew install fastlane
                '''
            }
        }
        stage('Pre-Build') {
            steps {
                sh """
            	agvtool new-version -all ${params.BUILD_NUMBER}
            	agvtool new-marketing-version ${params.VERSION}
            	fastlane spaceauth -u Аккаунт_в_Apple_Developer_Program
            	echo n
               """
            }
        }
        stage('Build') {
            steps {
                sh '''
                    xcodebuild -resolvePackageDependencies CI_CD_Exploration.xcodeproj/project.xcworkspace -scheme CI_CD_Exploration -destination 'platform=iOS Simulator,name=Any iOS Simulator Device' -derivedDataPath Build/ -configuration Debug
                '''
            }
        }
    }
}