# Kubernetes Dashboard (Web UI)
Dashboard is a web-based Kubernetes user interface. We can use Dashboard to get an overview of applications running on our cluster, as well as for creating or modifying individual Kubernetes resources.Dashboard also provides information on the state of Kubernetes resources in your cluster and on any errors that may have occurred.

#### Configuration Steps:

or https://www.programmersought.com/article/63956807837/
bypass authentication : https://devblogs.microsoft.com/premier-developer/bypassing-authentication-for-the-local-kubernetes-cluster-dashboard/

1. Deploy the Kubernetes Dashboard UI:

    `kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0/aio/deploy/recommended.yaml`

2. Run `kubectl apply -f dashboard-adminuser.yml` to create a new user.
3. Run `kubectl proxy` to access the Dashboard UI. or  kubectl proxy --address 0.0.0.0 --accept-hosts '.*'
. Note that this is a possible security vulnerability as you are accepting all traffic (AWS firewall rules) and also all connections for your kubectl proxy (--address 0.0.0.0 --accept-hosts '.*') so please narrow it down or use different approach. If you have more questions feel free to ask.

4. Visit http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/
5. Get a token by running the following command and copy the token into your clipboard.

    `kubectl -n kubernetes-dashboard get secret $(kubectl -n kubernetes-dashboard get sa/admin-user -o jsonpath="{.secrets[0].name}") -o go-template="{{.data.token | base64decode}}"`

6. Paste the token into the login screen and you can then sign in to the dashboard.

#### To create a resource from dashboard:
8. Click on + and then upload the newDeploy.yml manifest file. This will create a new deployment resource for us. 

#### Useful Reference links:
- [Deploying Dashboard UI](https://kubernetes.io/docs/tasks/access-application-cluster/web-ui-dashboard/#deploying-the-dashboard-ui)
- [Creating Sample User](https://github.com/kubernetes/dashboard/blob/master/docs/user/access-control/creating-sample-user.md)
-[Official Dashboard Github Repository](https://github.com/kubernetes/dashboard/)
