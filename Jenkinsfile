node {
    def server = Artifactory.server 'myjfrogtutorial'
    def rtNpm = Artifactory.newNpmBuild()
    def buildInfo

    stage ('Clone') {
        git url: 'https://github.com/jfrog/project-examples.git'
    }

    stage ('Artifactory configuration') {
        rtNpm.deployer repo: 'my-npm', server: server
        rtNpm.resolver repo: 'my-npm', server: server
        rtNpm.tool = 'npm' // Tool name from Jenkins configuration
        buildInfo = Artifactory.newBuildInfo()
    }

    stage ('Install npm') {
        rtNpm.install buildInfo: buildInfo, path: 'npm-example'
    }

    stage ('Publish npm') {
        rtNpm.publish buildInfo: buildInfo, path: 'npm-example'
    }

    stage ('Publish build info') {
        server.publishBuildInfo buildInfo
    }
}
