pipeline {
    agent any

    stages {
        stage('pull code') {
            steps {
                git branch: 'main', credentialsId: 'github-ssh', url: 'git@github.com:yezi60/onlines-store.git'
            }
        }
        stage('build project') {
            steps {
                sh '''echo "运行 cnpm install"
                cnpm install
                echo "运行 cnpm run build"
                cnpm run build
                echo "构建成功"'''
            }
        }
        stage('deploy project') {
            steps {
                sshPublisher(publishers: [sshPublisherDesc(configName: '1080ti server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'echo "success"', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '/docker/nginx/data/html/shop', remoteDirectorySDF: false, removePrefix: 'dist', sourceFiles: 'dist/**')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
            }
        }
    }
}
