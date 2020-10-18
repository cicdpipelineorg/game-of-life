def imagename = "354309344841.dkr.ecr.us-east-1.amazonaws.com/sujith:$BUILD_NUMBER"
def registryCredential = 'ecr:us-east-1:awsecr'
def dockerImage = ''
node('DOCKER')
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
docker.withRegistry( 'https://354309344841.dkr.ecr.us-east-1.amazonaws.com', registryCredential ) {
dockerImage.push()
}
}
stage('cleaning up')
{
sh "docker rmi $imagename"
}
}
