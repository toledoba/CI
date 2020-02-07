#!/usr/bin/env groovy
pipeline {
    agent any
    
    stages {
        stage('widoco') {
            steps {
                script {
                    tags_extra = "value_1"
                }
                echo "tags_extra: ${tags_extra}"
				sh "./widoco.sh"
            }
        }
        stage('stage two') {
            steps {
                echo "tags_extra: ${tags_extra}"
            }
        }
        stage('stage three') {
            when {
                expression { tags_extra != 'bla' }
            }
            steps {
                echo "tags_extra: ${tags_extra}"
            }
        }
    }
}