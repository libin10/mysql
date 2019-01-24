#!/usr/bin/groovy
@Library('github.com/stakater/fabric8-pipeline-library@master')

def dummy = ""

prepareAndUploadCharts {
    charts = [ "mysql-storage","mysql" ]
    chartRepositoryURL = 'https://chartmuseum.release.stakater.com'
    publicChartRepositoryURL = 'https://stakater.github.io/stakater-charts'
    publicChartGitURL = 'git@github.com:stakater/stakater-charts.git'
}
