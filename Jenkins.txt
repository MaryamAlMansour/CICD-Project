cd /opt
docker image build -t $JOB_NAME -t  $JOB_NAME:v1.$BUILD_ID .
docker image tag $JOB_NAME:v1.$BUILD_ID NadirTech1/$JOB_NAME:v1.$BUILD_ID
docker image tag $JOB_NAME:v1.$BUILD_ID NadirTech1/$JOB_NAME:latest
docker image push NadirTech1/$JOB_NAME:v1.$BUILD_ID
docker image push NadirTech1/$JOB_NAME:latest
docker image rmi $JOB_NAME:v1.$BUILD_ID NadirTech1/$JOB_NAME:v1.$BUILD_ID NadirTech1/$JOB_NAME:lates
