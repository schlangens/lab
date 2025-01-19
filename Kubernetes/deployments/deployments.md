## Deployments
Used to deploy ReplicaSet (RS) - Orchestrates pods.

``k create deployment -h | less``

``kubectrl create deployment my-dep --image=nginx --replicas=3``

A deployment is a ways to define a desired state in kubernetes.

``k create deploy test --image=httpd --replicas=3``
``k get deployment.apps``

This is how you edit the deployment
``k edit deployment.apps``

# Now lets do this from code
Delete the previous deployment
``k delete deployment.apps test``

Now lets create a deployment YAML code
``k create deploy --image=httpd --replicas=10 --dry-run=client -o yaml > first-deployment.yaml``

Little trick in VIM since we have in our bashrc file you can hit ``esc`` then``k`` to print the last command. You can also enter the up arrow.

Lets clean up the new YAML
- Remove creation time (dd)
- Strategy - We will get into this later
- Resources, Status

Now lets apply to cluster
``k apply -f first-deployment.yaml``
``k get deployment.apps``

``k describe deployment.apps first-deployment``
This will give you the name of the (RS) - Replica Set

``k get replicasets.app``
This will show the RS.

``k describe replicasets.app <tab>``
Check out the file Annotations.
Something to be aware of is old images of RS are kept on node. The default setting is 10.

Now lets open the help file in Vim
``k create deploy -h | vim -``
This ``-`` sends input to VIM

You are not able to edit strategy from the create deploy, edit from ``k edit deployment.apps first-deployment``

Minimum availability is dictated by the parameters specified in the deployment strategy
https://kubernetes.io/docs/concepts/workloads/controllers/deployment/

``.spec.strategy`` specifies the strategy used to replace old Pods by new ones. ``.spec.strategy.type`` can be "Recreate" or "RollingUpdate". "RollingUpdate" is the default value.

Cool trick in vim to select the entire line ``shift v`` then use the ``< >`` on the keyboard to move indentation.

Change the tag to a older image in your yaml file
then ``watch -n 1 kgp`` or ``watch -n 1 kubectl get pods``
In tmux - ``ctrl+shift+'`` will split the window
Then in that pane run the update with your older tag applied inside your yaml deployment file.
``k apply -f first-deployment.yaml``

 In VIM if you want to delete all of the lines from you marker down
 you would hit ``d + shift-g``

In bash you can check the last exit code ``echo $``

Anything other that 0 is an error code







