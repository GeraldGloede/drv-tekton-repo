# Chapter 3: Creating Tasks in Tekton

Tasks are the smallest building blocks in a Tekton pipeline. In this chapter, we’ll show you how to create Tasks in Tekton and provide some examples to get you started.First let's create a directory for this lab and set it as the current working directory:

```
mkdir ~/Tekton
cd ~/Tekton
```

Now let's create our first `Task` by copying the following to a file named `echo-hello-world.yaml`:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: echo-hello-world
spec:
  steps:
    - name: echo
      image: registry.access.redhat.com/ubi8-minimal
      command:
        - echo
      args:
        - "Hello World"
```

Take a few seconds to review the `Task`. It is pretty straightforward when we look at it.
All we are asking the `Task` to do is to obtain our image module (the images that the task is using are actually the modules for our pipeline) and then it runs the echo command with the "Hello World" arguments.

Since a `Task` is a Kubernetes Custom Resource, we will go ahead and use the `oc` command to create it:

```
oc create -f echo-hello-world.yaml
```

We can also use the `tkn` command to list the task:

```
tkn task list
```

The output will be of the form:

```
NAME               DESCRIPTION   AGE
echo-hello-world                 X seconds ago
```

Now, In order to run the command we need to create a `TaskRun` custom resource. We can create it with a YAML file or by using the `tkn` command.

In order to create a YAML file, copy the following to a file named `tr-echo-hello-world.yaml`:

```yaml
apiVersion: tekton.dev/v1beta1
kind: TaskRun
metadata:
  name: taskrun-echo-hello-world
spec:
  taskRef:
    name: echo-hello-world
```

Now create the `TaskRun`:

```
oc create -f tr-echo-hello-world.yaml
```

Now that we created a the `TaskRun` for our `Task` we can view it using the CLI:

```
tkn taskrun list
```

To view the output of the `TaskRun` we can use the `tkn` tool:

```
tkn taskrun logs taskrun-echo-hello-world
```

The output should be of the form:

[echo] Hello World

In case the `Task` takes a long time to finish, we can look at the `pods` and their status:

```
oc get pods
```

The output will be of the form:

```
NAME                       STARTED         DURATION   STATUS
taskrun-echo-hello-world   7 seconds ago   ---        Running(Pending)
```

The pod has not yet started. Perhaps it is downloading the container image for the first time. When the task has completed, the output should be of the following form:

```
NAME                       STARTED         DURATION   STATUS
taskrun-echo-hello-world   3 minutes ago   26s        Succeeded
```

### Passing Parameters to Tasks

Now that we created a `Task` and a `TaskRun` we can go ahead and expand our `Task` by adding parameters to our task. `params` enable us to use the same `Task` for more than one resources which can be both the input and the output of a task.

Copy the following to a file named `task-hello-params.yaml`:

```yaml
apiVersion: tekton.dev/v1beta1
kind: Task
metadata:
  name: echo-hello-person
spec:
  params:
    - name: person
      description: Person to greet
      default: bob
  steps:
    - name: echo
      image: registry.redhat.io/ubi8/ubi-minimal
      script: |
        echo "Hello $(params.person)"
```

In our example we have configured a parameter named `person` and added it as one of our arguments.

Let's go ahead and run it:

```
oc create -f task-hello-params.yaml
```

Now that the `Task` has been created, we run it by creating a `TaskRun` resource using the `tkn` command as follows:

```
tkn task start --use-param-defaults echo-hello-person
```

When we ran the command the last line of the output is the command we need to view the logs and make sure it is running as we wanted.
Go ahead and run the logs command ...
What do you see?

Now let's change "bob" to "sally" ...
There are several ways to do it:

1. update the YAML file and apply the changes
2. edit the current task using the oc command
3. send a new `param` to another run

The first option is pretty simple, just edit the file and change the `default` person from "bob" to "sally" and then apply the changes using:

```
vi task-hello-params.yaml
```

and

```
oc apply -f task-hello-params.yaml
```

Question: Why was "apply" used here instead of "create"?

The second way to change the name is even more simple. Run the following command to open an editor with the current contents of the `Task` object:

```
oc get tasks -o name | grep person | xargs oc edit
```

Edit the name in the task. Once you save and exit the changes will take effect. Rerun the task.

The last way is preferred. We are going to create a `TaskRun` where we will define the param's new value in it. Copy the following to a file named `taskrun-hello-person-param-override.yaml`:

```yaml
apiVersion: tekton.dev/v1beta1
kind: TaskRun
metadata:
  name: echo-hello-person-task-run-override
spec:
  taskRef:
    name: echo-hello-person
  params:
    - name: person
      value: sally
```

Now create the `TaskRun`:

```
oc create -f taskrun-hello-person-param-override.yaml
```

Now we can look at the logs and see the output we wanted:

```
tkn taskrun logs echo-hello-person-task-run-override -f
```

If you see "Hello sally" then we are good to go.

## Bonus Task

Try sending the `param` value using the `tkn` command.

## Cleanup

After you haved completed all the tasks it is time for a cleanup:

```
oc get taskrun -o name | xargs oc delete
```

We will wait for the rest of the class to complete the lab and move on to Chapter 4
