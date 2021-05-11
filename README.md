Minimal Node.js application for intro to Docker tutorial: https://www.digitalocean.com/community/tutorials/how-to-build-a-node-js-application-with-docker

To deploy this app to eks we ave created three files 

deployment.yaml,service.yaml and ingress.yaml

application internal port : 8080
expose port for outside access: 80
node port:31110

Deployment steps : got to root folder 

kubectl apply -f deployment.yaml

kubectl get pods # to check pod created successfully

kubectl apply -f service.yaml

kubectl get svc # to get the url of Loadbalancer 

to add ingress:
---------------

helm repo add stable https://charts.helm.sh/stable

helm repo add incubator https://charts.helm.sh/incubator

helm install ingress incubator/aws-alb-ingress-controller   --set autoDiscoverAwsRegion=true   --set autoDiscoverAwsVpcID=true   --set clusterName=my-cluster

kubectl get pods -l "app.kubernetes.io/instance=ingress" # to check ingress servcie created 

kubectl apply -f ingress.yaml

kubectl describe ingress hello-kubernetes # to get the url of loadbalancer

