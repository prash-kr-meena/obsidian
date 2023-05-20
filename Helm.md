What is Minikube?
Why we use it?
How to install?
How does it work?
[[Resetting Minikube]]




What is helm?
Why we use it?
How to install helm?
Why is helm 3 very different from helm 2?


What is artifact hub?

what is oci registries? while downloading helm https://github.com/helm/helm/releases 

from `helm env` we can get the location details

where does helm stores the details of the repository?

`/Library/Preferences/helm`


and where does helm actually stores the chart that we pull from those repositories?

`/Users/prashant.me/Library/Caches/helm/repository`





how to see all the values of the chart that we can customize for a chart inside the repo?

`helm show values prometheus-community/kube-prometheus-stack`

we can export it into a file
` helm show values prometheus-community/kube-prometheus-stack  > valuse.yaml`

Note: this is not a kubernetes yaml file, we can't apply file to kubernetes 

I.e. **kubectl apply -f values.yaml**
will result in error

kubernetes does not recognizes this file
but helm does











