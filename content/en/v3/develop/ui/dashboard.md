---
title: Dashboard
linktitle: Dashboard
type: docs
description: Read only dashboard view of pipelines and logs
weight: 100
aliases:
  - /v3/develop/ui/dashboard
---

It's a common requirement to want to view pipelines running, their logs or to be able to click on a Pull Request on your git provider and view the pipeline log for that commit on that Pull Request.

To implement this we include the [jx-pipelines-visualizer](https://github.com/jenkins-x/jx-pipelines-visualizer) application inside Jenkins X.

This provides a simple read only web UI for viewing pipelines and pipeline logs and its linked automatically with any Pull Request you create on repositories managed by Jenkins X.

### Accessing the Pipelines Visualizer

If you [have a recent jx binary](/v3/guides/upgrade/#cli) run:

```bash 
jx dash
``` 

and it will open the dashboard using the basic authentication login and password.

![](/images/jx-pipelines-visualizer/v1-home.png)

### Viewing from a Pull Request or from a release

If you create a Pull Request on a git repository you have [created or imported](/v3/develop/create-project/) in Jenkins X you should see a link on the Pull Request. 

Here's an example - see the **Details** link on the right of the Pull Request pipeline:

<img src="/images/quickstart/pr-link.png" class="img-thumbnail">

And in the home page of the repository, by clicking on the little orange icon preceding the last commit id you'll open the view of the running pipeline(s) on your release with the link to their respective **Details** link(s):

c8021ccecb314584b53633f51140dd0f.png![image](https://user-images.githubusercontent.com/52448671/114937449-1a387280-9e3e-11eb-8af0-c8011de33a7b.png)  
  

Clicking the **Details** link should open the [jx-pipelines-visualizer](https://github.com/jenkins-x/jx-pipelines-visualizer) UI for this pipeline build.

![](/images/jx-pipelines-visualizer/v1-pipeline-success.png)

### Logging in to the Pipelines Visualizer

Unless you [customize the chart](/v3/develop/apps/#customising-charts) to change the `Ingress` the default will use _basic authentication_ to access the web UI to avoid your pipeline logs being visible on the internet.

The default username is `admin`. 

To find the generated random password to access the UI type:

```bash 
jx ns jx
kubectl get secret jx-basic-auth-user-password -o jsonpath="{.data.password}" | base64 --decode
```

That should display the randomly generated password.

If you type the username and password into your browser it should open the dashboard.

### Pipelines Traces

If you [enable the observability stack](/v3/admin/guides/observability/), then you will get a new link **Trace** in your pipeline view - once the pipeline is finished - that will open the pipeline trace in Grafana so that you can see the timings of each stage and steps in your pipeline:

![](/images/jx-pipelines-visualizer/pipeline-trace.gif)
