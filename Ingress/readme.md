# Ingress

Ingress is a Kubernetes API object that provides a way to manage external access to services running in a Kubernetes cluster. In other words, it allows you to expose your services to the internet or other parts of your infrastructure outside of the Kubernetes cluster.


There are several ways to implement Ingress in Kubernetes, including using built-in Ingress controllers such as Nginx or Traefik, or using third-party solutions like Istio or Ambassador.

To use Ingress in your Kubernetes cluster, you will need to follow these steps:

- Choose an Ingress controller: Select an Ingress controller that suits your needs, or use the built-in Kubernetes Ingress controller.

**Nginx Controller using HELM** 
```bash 
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
```

- Deploy the Ingress controller: Deploy the selected Ingress controller to your cluster. This will typically involve creating a deployment and service object for the controller. But here we are using helm for it.

```bash
helm install nginx-ingress ingress-nginx/ingress-nginx
```

- Define Ingress rules: Create Ingress objects that define the rules for routing traffic to your services. These rules are defined using annotations on the Ingress object.

```bash
kubectl apply -f ingress.yaml
```


- Configure DNS: Point your domain name to the IP address of the load balancer or ingress controller service.

I have used Azure load balancer and domain name to access the application.

<!--  <IMAGE HERE> -->

The load balancer is configured to route traffic to the nodes in the cluster. The nodes then route traffic to the ingress controller service, which then routes traffic to the correct service based on the rules defined in the Ingress object.

- Test and troubleshoot: Test your Ingress configuration and troubleshoot any issues that arise.