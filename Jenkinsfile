#!/usr/bin/groovy
@Library('github.com/stakater/fabric8-pipeline-library@master')

String mysqlPackageName = ""
String mysqlStoragePackageName = ""
String mysqlChartName = "mysql"
String mysqlStorageChartName = "mysql-storage"

clientsNode(clientsImage: 'stakater/pipeline-tools:dev') {
    container(name: 'clients') {
        def helm = new io.stakater.charts.Helm()
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
            chartManager.uploadToChartMuseum(WORKSPACE, mysqlChartName, mysqlPackageName)
            chartManager.uploadToChartMuseum(WORKSPACE, mysqlStorageChartName, mysqlStoragePackageName)
        }
    }
}
