node("docker") {
    docker.withRegistry('bihanc', 'docker-hub') {
    
        git url: "https://github.com/uchanbi/test-app.git", credentialsId: 'github'
    
        sh "git rev-parse HEAD > .git/commit-id"
        def commit_id = readFile('.git/commit-id').trim()
        println commit_id
    
        stage "build"
        def app = docker.build "airport"
    
        stage "publish"
        app.push 'master'
        app.push "${commit_id}"
    }
}
