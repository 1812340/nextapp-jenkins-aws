node{
    def appDir = "/var/www/nextjs-app"

    stage("clean workspace"){
     echo "cleaning jenkins workspace"
        deleteDir()
    }
    stage("Clone repository"){
        echo "cloning repository"
        git (
            branch: 'main',
            url: "https://github.com/1812340/nextapp-jenkins-aws"
        )
    }
    stage("Deploying on EC2"){
        echo "Deploying on Ec2"
        sh """
            sudo mkdir -p ${appDir}
            sudo chown -R jenkins:jenkins ${appDir}

            rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${appDir}

            cd ${appDir}
            sudo npm install
            sudo npm run build
            sudo fuser -k 3000/tcp || true
            npm run start
        """
    }

}