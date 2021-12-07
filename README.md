# jenkins-flask-k8s

This is a demo fro CI/CD of Python Flask app to Kubernetes.

Prerequisite Steps:
Install minikube and Docker Desktop

Start Minikube cluster:

    minikube start

You need to run as well:

    minikube docker-env

In Powershell run:

    Invoke-Expression -Command "minikube -p minikube docker-env"

In CMD run:

    @FOR /f "tokens=*" %i IN ('minikube -p minikube docker-env') DO @%i

In bash run:

    eval $(minikube -p minikube docker-env)

Then run:

    cd jenkins-minikube
    docker image build -t myjenkins .
    kubectl apply -f jenkins.yaml
    kubectl get all
    minikube ip

So you can access Jenkins docker container via ip and port 31000. If it's not working, use:

    minikube service jenkins --url

And then try the URL from output.

Then in Jenkins UI from browser in "Manage Jenkins" page enter to environmental variables on global properties:

    ORGANIZATION_NAME (username on GitHub)
    YOUR_DOCKERHUB_USERNAME (optional, there is no any push to container registry)

Then add new item with name "webapp" and select Multibranch Pipeline Option and click the save option.

Enter display name as "webapp"

Then go to the Branch Configuration section and click on Add source button, once you click the add button, you get a dropdown with some options to choose from, you have to pick Jenkins as we want Jenkins wide global credentials to be applicable across the organization repo.

Enter your GitHub username and secret for password along with ID name. ID must be GitHub, according to deployment configuration.

After saving pipeline will run and you can achive hello-world Python webapp using

    minikube service jenkins --url

or ip address from

    minikube ip

and port from

    kubectl get all

for jenkins-flask-k8s service.