# jenkins-flask-k8s

This is a demo fro CI/CD of Python Flask app to Kubernetes.

Prerequisite Steps:
Install minikube and Docker Desktop

Start Minikube cluster: minikube start

You need to run as well:
minikube docker-env

In Powershell also run:
Invoke-Expression -Command "minikube -p minikube docker-env"

In CMD also run:
@FOR /f "tokens=*" %i IN ('minikube -p minikube docker-env') DO @%i

Than run:
cd jenkins-minikube
docker image build -t myjenkins .
kubectl apply -f jenkins.yaml
kubectl get all
minikube ip

So you can access Jenkins docker container via ip and port 31000. If it's not working, use:

minikube service jenkins --url

And then try the URL from output.