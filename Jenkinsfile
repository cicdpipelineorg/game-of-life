def imagename = "sujith140/gameoflife:$BUILD_NUMBER"
def registryCredential = 'dockerhubfinal'
def dockerImage = ''
node('docker')
{
stage('git')
{
git url: 'https://github.com/cicdpipelineorg/game-of-life.git', branch: 'master'
}
stage('building image')
{

dockerImage = docker.build imagename
}

stage('push image to repository')
{
docker.withRegistry( '', registryCredential ) {
dockerImage.push()
}
}
stage('cleaning up')
{
sh "docker rmi $imagename"
}
}
node('kubernetes')
{
    stage('deploying to kubernetes')
{
    git url: 'https://github.com/sujith140/kubernetes.git', branch: 'master'
    sh 'envsubst < gameoflife.yaml | kubectl apply -f -' 
}

}
