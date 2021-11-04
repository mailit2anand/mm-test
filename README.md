# mm-test
sample.war is the sample application which can be deployed in atomcat container.
Start a minikube cluster.
Put the Dockerfile in the same location as that of the war file
minikube image build -t sampleapp .   --> This command will containerize the sample.war in the tomcat container.
kubectl create -f sample-app-pv.yaml -- > This will create the pv required for storing the logs.
kubectl create -f sample-app-pvc.yaml  --> This will create the pvc.
kubectl apply -f sample-app-deployment.yaml  --> This will deploy the app in the minikube cluster
kubectl apply -f sample-app-service.yaml  --> This will create the service in minikube cluster
kubectl expose deployment sampleapp-deploy --port=80  --> This will expose the deployment to external.
minikube addons enable ingress  --> This will deploy an ingress-controller in the minikube cluster.
openssl req -x509 -newkey rsa:4096 -sha256 -nodes -keyout tls_self.key -out tls_self.crt -subj "/CN=*.sampleapp-mmtest" -days 365  --> This will create the key pair.
kubectl create secret tls sampleapp-secret --cert=tls_self.crt --key=tls_self.key --> This will creat the secret with the keypair
kubectl apply -f sample-app-ingress.yaml --> This will deploy the ingress resource for the sample app.

