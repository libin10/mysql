#!/usr/bin/groovy
@Library('github.com/stakater/fabric8-pipeline-library@master')

String mysqlPackageName = ""
String mysqlStoragePackageName = ""
String mysqlChartName = "mysql"
String mysqlStorageChartName = "mysql-storage"

toolsNode(toolsImage: 'stakater/pipeline-tools:1.2.0') {
    container(name: 'tools') {
        def helm = new io.stakater.charts.Helm()
        def common = new io.stakater.Common()
        def chartManager = new io.stakater.charts.ChartManager()
        stage('Checkout') {
            checkout scm
        }
        
        stage('Init Helm') {
            helm.init(true)
        }

        stage('Prepare Chart') {
            helm.lint(WORKSPACE, mysqlChartName)
            mysqlPackageName = helm.package(WORKSPACE, mysqlChartName)

            helm.lint(WORKSPACE, mysqlStorageChartName)
            mysqlStoragePackageName = helm.package(WORKSPACE, mysqlStorageChartName)
        }

        stage('Upload Chart') {
            String cmUsername = common.getEnvValue('CHARTMUSEUM_USERNAME')
            String cmPassword = common.getEnvValue('CHARTMUSEUM_PASSWORD')
            chartManager.uploadToChartMuseum(WORKSPACE, mysqlChartName, mysqlPackageName, cmUsername, cmPassword)
            chartManager.uploadToChartMuseum(WORKSPACE, mysqlStorageChartName, mysqlStoragePackageName, cmUsername, cmPassword)
        }
    }
}
