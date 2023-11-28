##TODO
* Add links 
	* Kops
	* kiam
	* External Secrets
	* OIDC blogs

Recently, we upgraded our Kubernetes clusters. We jumped from version 1.19 to 1.25 and this jump had a _lot_ of huge changes that went in to it.  This tale is a bit twisted and convoluted but in the end it weaves together into some kind of tapestry? Anyhow - enjoy

### Background
We set up our initial K8s clusters using kOps and K8s version 1.17. We created 3 clusters, a test cluster(for the infrastructure team to play with) a staging cluster(for development teams to use) and the production (for the money making) all with pretty basic configurations. An instance group of masters, and an instance group of nodes. We soon changed it to 3 instance groups spread across 3 AWS availability zones. We utilized the nginx ingress to handle routing management and the AWS ALB ingress for creating a single ALB with the appropriate certs. Individual apps would deploy their own replicas, and ingress objects which would get handled by Nginx.

About 8 months after setting this up my team got handed a newly acquired set of infrastructure to manage, so of course we set about re-creating this setup. Of course took the latest version of everything, which at the time was 1.21, and heres where things get interesting. 

### AWS and K8s playing nice
Starting with K8s 1.21 there came about some changes with how AWS allowed things to determine IAM roles. Before, we were using kIAM which allowed services to use the ec2 metadata and assume a set of known roles, controlled by the kube services themselves. AWS changed how they allowed things to assume roles, and thus breaking how kIAM worked. Instead kOPS now created roles in AWS and you can associate them with k8s service accounts.

### External secrets
We have been using AWS external secrets to manage configuration data. There was a third party add-on for syncing the secrets from AWS Secrets Manager to 


