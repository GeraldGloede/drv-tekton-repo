# Chapter 2: Installing RedHat Pipelines Operator with the web Console and the cli:

## Installing OpenShift Pipelines

- [Installing the OpenShift Pipelines Operator using the CLI](https://docs.openshift.com/container-platform/4.12/cicd/pipelines/installing-pipelines.html#op-installing-pipelines-operator-using-the-cli_installing-pipelines)
- [Red Hat OpenShift Pipelines Operator in a restricted environment](https://docs.openshift.com/container-platform/4.12/cicd/pipelines/installing-pipelines.html#op-pipelines-operator-in-restricted-environment_installing-pipelines)
- [Disabling the automatic creation of RBAC resources](https://docs.openshift.com/container-platform/4.12/cicd/pipelines/installing-pipelines.html#op-disabling-automatic-creation-of-rbac-resources_installing-pipelines)

This guide walks cluster administrators through the process of installing the Red Hat OpenShift Pipelines Operator to an OpenShift Container Platform cluster.

## Prerequisites

- You have access to an OpenShift Container Platform cluster using an account with `cluster-admin` permissions.

- You have installed `oc` CLI.

- You have installed [OpenShift Pipelines (`tkn`) CLI](https://docs.openshift.com/container-platform/4.12/cli_reference/tkn_cli/installing-tkn.html#installing-tkn) on your local system.

# Installing tkn client

- [Installing the Red Hat OpenShift Pipelines CLI on Linux](https://docs.openshift.com/container-platform/4.12/cli_reference/tkn_cli/installing-tkn.html#installing-tkn-on-linux)
- [Installing the Red Hat OpenShift Pipelines CLI on Linux using an RPM](https://docs.openshift.com/container-platform/4.12/cli_reference/tkn_cli/installing-tkn.html#installing-tkn-on-linux-using-rpm)
- [Installing the Red Hat OpenShift Pipelines CLI on Windows](https://docs.openshift.com/container-platform/4.12/cli_reference/tkn_cli/installing-tkn.html#installing-tkn-on-windows)
- [Installing the Red Hat OpenShift Pipelines CLI on macOS](https://docs.openshift.com/container-platform/4.12/cli_reference/tkn_cli/installing-tkn.html#installing-tkn-on-macos)

Use the CLI tool to manage Red Hat OpenShift Pipelines from a terminal. The following section describes how to install the CLI tool on different platforms.

You can also find the URL to the latest binaries from the OpenShift Container Platform web console by clicking the **?** icon in the upper-right corner and selecting **Command Line Tools**.

## Important Information!!!

Running Red Hat OpenShift Pipelines on ARM hardware is a Technology Preview feature only. Technology Preview features are not supported with Red Hat production service level agreements (SLAs) and might not be functionally complete. Red Hat does not recommend using them in production. These features provide early access to upcoming product features, enabling customers to test functionality and provide feedback during the development process.

For more information about the support scope of Red Hat Technology Preview features, see [Technology Preview Features Support Scope](https://access.redhat.com/support/offerings/techpreview/).

Both the archives and the RPMs contain the following executables:

- tkn
- tkn-pac
- opc

Running Red Hat OpenShift Pipelines with the `opc` CLI tool is a Technology Preview feature only. Technology Preview features are not supported with Red Hat production service level agreements (SLAs) and might not be functionally complete. Red Hat does not recommend using them in production. These features provide early access to upcoming product features, enabling customers to test functionality and provide feedback during the development process.

For more information about the support scope of Red Hat Technology Preview features, see [Technology Preview Features Support Scope](https://access.redhat.com/support/offerings/techpreview/).

## Installing the Red Hat OpenShift Pipelines CLI on Linux

For Linux distributions, you can download the CLI as a `tar.gz` archive.

Procedure

1. Download the relevant CLI tool.
   
   - [Linux (x86_64, amd64)](https://mirror.openshift.com/pub/openshift-v4/clients/pipeline/1.9.1/tkn-linux-amd64.tar.gz)
   
   - [Linux on IBM zSystems and IBM® LinuxONE (s390x)](https://mirror.openshift.com/pub/openshift-v4/clients/pipeline/1.9.1/tkn-linux-s390x.tar.gz)
   
   - [Linux on IBM Power (ppc64le)](https://mirror.openshift.com/pub/openshift-v4/clients/pipeline/1.9.1/tkn-linux-ppc64le.tar.gz)
   
   - [Linux on ARM (arm64)](https://mirror.openshift.com/pub/openshift-v4/clients/pipeline/1.9.1/tkn-linux-arm64.tar.gz)

2. Unpack the archive:
   
   ```
   $ tar xvzf <file>
   ```

3. Add the location of your `tkn`, `tkn-pac`, and `opc` files to your `PATH` environment variable.

4. To check your `PATH`, run the following command:
   
   ```
   $ echo $PATH
   ```

## Installing the Red Hat OpenShift Pipelines CLI on Linux using an RPM

For Red Hat Enterprise Linux (RHEL) version 8, you can install the Red Hat OpenShift Pipelines CLI as an RPM.

Prerequisites

- You have an active OpenShift Container Platform subscription on your Red Hat account.

- You have root or sudo privileges on your local system.

Procedure

1. Register with Red Hat Subscription Manager:
   
   ```
   # subscription-manager register
   ```

2. Pull the latest subscription data:
   
   ```
   # subscription-manager refresh
   ```

3. List the available subscriptions:
   
   ```
   # subscription-manager list --available --matches '*pipelines*'
   ```

4. In the output for the previous command, find the pool ID for your OpenShift Container Platform subscription and attach the subscription to the registered system:
   
   ```
   # subscription-manager attach --pool=<pool_id>
   ```

5. Enable the repositories required by Red Hat OpenShift Pipelines:
   
   - Linux (x86_64, amd64)
     
     ```
     # subscription-manager repos --enable="pipelines-1.9-for-rhel-8-x86_64-rpms"
     ```
   
   - Linux on IBM Z and LinuxONE (s390x)
     
     ```
     # subscription-manager repos --enable="pipelines-1.9-for-rhel-8-s390x-rpms"
     ```
   
   - Linux on IBM Power (ppc64le)
     
     ```
     # subscription-manager repos --enable="pipelines-1.9-for-rhel-8-ppc64le-rpms"
     ```
   
   - Linux on ARM (arm64)
     
     ```
     # subscription-manager repos --enable="pipelines-1.9-for-rhel-8-arm64-rpms"
     ```

6. Install the `openshift-pipelines-client` package:
   
   ```
   # yum install openshift-pipelines-client
   ```

After you install the CLI, it is available using the `tkn` command:

```
$ tkn version
```

## Installing the Red Hat OpenShift Pipelines CLI on Windows

For Windows, you can download the CLI as a `zip` archive.

Procedure

1. Download the [CLI tool](https://mirror.openshift.com/pub/openshift-v4/clients/pipeline/1.9.1/tkn-windows-amd64.zip).

2. Extract the archive with a ZIP program.

3. Add the location of your `tkn`, `tkn-pac`, and `opc` files to your `PATH` environment variable.

4. To check your `PATH`, run the following command:
   
   ```
   C:\> path
   ```

## Installing the Red Hat OpenShift Pipelines CLI on macOS

For macOS, you can download the CLI as a `tar.gz` archive.

Procedure

1. Download the relevant CLI tool.
   
   - [macOS](https://mirror.openshift.com/pub/openshift-v4/clients/pipeline/1.9.1/tkn-macos-amd64.tar.gz)
   
   - [macOS on ARM](https://mirror.openshift.com/pub/openshift-v4/clients/pipeline/1.9.1/tkn-macos-arm64.tar.gz)

2. Unpack and extract the archive.

3. Add the location of your `tkn`, `tkn-pac`, and `opc` files to your `PATH` environment variable.

4. To check your `PATH`, run the following command:
   
   ```
   $ echo $PATH
   ```
- Your cluster has the [Marketplace capability](https://docs.openshift.com/container-platform/4.12/installing/cluster-capabilities.html#marketplace-operator_cluster-capabilities) enabled or the Red Hat Operator catalog source configured manually.

## Installing the Red Hat OpenShift Pipelines Operator in web console

You can install Red Hat OpenShift Pipelines using the Operator listed in the OpenShift Container Platform OperatorHub. When you install the Red Hat OpenShift Pipelines Operator, the custom resources (CRs) required for the pipelines configuration are automatically installed along with the Operator.

The default Operator custom resource definition (CRD) `config.operator.tekton.dev` is now replaced by `tektonconfigs.operator.tekton.dev`. In addition, the Operator provides the following additional CRDs to individually manage OpenShift Pipelines components:`tektonpipelines.operator.tekton.dev`, `tektontriggers.operator.tekton.dev` and `tektonaddons.operator.tekton.dev`.

If you have OpenShift Pipelines already installed on your cluster, the existing installation is seamlessly upgraded. The Operator will replace the instance of `config.operator.tekton.dev` on your cluster with an instance of `tektonconfigs.operator.tekton.dev` and additional objects of the other CRDs as necessary.

|     | If you manually changed your existing installation, such as, changing the target namespace in the `config.operator.tekton.dev` CRD instance by making changes to the `resource name - cluster`field, then the upgrade path is not smooth. In such cases, the recommended workflow is to uninstall your installation and reinstall the Red Hat OpenShift Pipelines Operator. |
| --- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

The Red Hat OpenShift Pipelines Operator now provides the option to choose the components that you want to install by specifying profiles as part of the `TektonConfig` CR. The `TektonConfig` CR is automatically installed when the Operator is installed. The supported profiles are:

- Lite: This installs only Tekton Pipelines.

- Basic: This installs Tekton Pipelines and Tekton Triggers.

- All: This is the default profile used when the `TektonConfig` CR is installed. This profile installs all of the Tekton components: Tekton Pipelines, Tekton Triggers, Tekton Addons (which include `ClusterTasks`, `ClusterTriggerBindings`, `ConsoleCLIDownload`, `ConsoleQuickStart` and `ConsoleYAMLSample` resources).

Procedure

1. In the **Administrator** perspective of the web console, navigate to **Operators** → **OperatorHub**.

2. Use the **Filter by keyword** box to search for `Red Hat OpenShift Pipelines` Operator in the catalog. Click the **Red Hat OpenShift Pipelines** Operator tile.

3. Read the brief description about the Operator on the **Red Hat OpenShift Pipelines** Operator page. Click **Install**.

4. On the **Install Operator** page:
   
   1. Select **All namespaces on the cluster (default)** for the **Installation Mode**. This mode installs the Operator in the default `openshift-operators` namespace, which enables the Operator to watch and be made available to all namespaces in the cluster.
   
   2. Select **Automatic** for the **Approval Strategy**. This ensures that the future upgrades to the Operator are handled automatically by the Operator Lifecycle Manager (OLM). If you select the **Manual** approval strategy, OLM creates an update request. As a cluster administrator, you must then manually approve the OLM update request to update the Operator to the new version.
   
   3. Select an **Update Channel**.
      
      - The `latest` channel enables installation of the most recent stable version of the Red Hat OpenShift Pipelines Operator. Currently, it is the default channel for installing the Red Hat OpenShift Pipelines Operator.
      
      - To install a specific version of the Red Hat OpenShift Pipelines Operator, cluster administrators can use the corresponding `pipelines-<version>` channel. For example, to install the Red Hat OpenShift Pipelines Operator version `1.8.x`, you can use the `pipelines-1.8` channel.

```
|     | Starting with OpenShift Container Platform 4.11, the `preview` and `stable` channels for installing and upgrading the Red Hat OpenShift Pipelines Operator are not available. However, in OpenShift Container Platform 4.10 and earlier versions, you can use the `preview` and `stable` channels for installing and upgrading the Operator. |
| --- | --- |
```

5. Click **Install**. You will see the Operator listed on the **Installed Operators** page.
   
   |     | The Operator is installed automatically into the `openshift-operators` namespace. |
   | --- | --------------------------------------------------------------------------------- |

6. Verify that the **Status** is set to **Succeeded Up to date** to confirm successful installation of Red Hat OpenShift Pipelines Operator.

## Installing the OpenShift Pipelines Operator using the CLI

You can install Red Hat OpenShift Pipelines Operator from the OperatorHub using the CLI.

Procedure

1. Create a Subscription object YAML file to subscribe a namespace to the Red Hat OpenShift Pipelines Operator, for example, `sub.yaml`:
   
   Example Subscription
   
   ```
   apiVersion: operators.coreos.com/v1alpha1
   kind: Subscription
   metadata:
   name: openshift-pipelines-operator
   namespace: openshift-operators
   spec:
   channel:  <channel name> 
   name: openshift-pipelines-operator-rh 
   source: redhat-operators 
   sourceNamespace: openshift-marketplace 
   ```
   
   |     | The channel name of the Operator. The `pipelines-<version>` channel is the default channel. For example, the default channel for Red Hat OpenShift Pipelines Operator version `1.7` is `pipelines-1.7`. The `latest` channel enables installation of the most recent stable version of the Red Hat OpenShift Pipelines Operator. |
   | --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
   |     | Name of the Operator to subscribe to.                                                                                                                                                                                                                                                                                            |
   |     | Name of the CatalogSource that provides the Operator.                                                                                                                                                                                                                                                                            |
   |     | Namespace of the CatalogSource. Use `openshift-marketplace` for the default OperatorHub CatalogSources.                                                                                                                                                                                                                          |

2. Create the Subscription object:
   
   $ oc apply -f sub.yaml
   
   The Red Hat OpenShift Pipelines Operator is now installed in the default target namespace `openshift-operators`.

## Red Hat OpenShift Pipelines Operator in a restricted environment

The Red Hat OpenShift Pipelines Operator enables support for installation of pipelines in a restricted network environment.

The Operator installs a proxy webhook that sets the proxy environment variables in the containers of the pod created by tekton-controllers based on the `cluster` proxy object. It also sets the proxy environment variables in the `TektonPipelines`, `TektonTriggers`, `Controllers`, `Webhooks`, and `Operator Proxy Webhook` resources.

By default, the proxy webhook is disabled for the `openshift-pipelines` namespace. To disable it for any other namespace, you can add the `operator.tekton.dev/disable-proxy: true` label to the `namespace` object.

## Disabling the automatic creation of RBAC resources

The default installation of the Red Hat OpenShift Pipelines Operator creates multiple role-based access control (RBAC) resources for all namespaces in the cluster, except the namespaces matching the `^(openshift|kube)-*` regular expression pattern. Among these RBAC resources, the `pipelines-scc-rolebinding` security context constraint (SCC) role binding resource is a potential security issue, because the associated `pipelines-scc` SCC has the `RunAsAny` privilege.

To disable the automatic creation of cluster-wide RBAC resources after the Red Hat OpenShift Pipelines Operator is installed, cluster administrators can set the `createRbacResource` parameter to `false` in the cluster-level `TektonConfig` custom resource (CR).

Example `TektonConfig` CR

```
apiVersion: operator.tekton.dev/v1alpha1
kind: TektonConfig
metadata:
  name: config
spec:
  params:
  - name: createRbacResource
    value: "false"
  profile: all
  targetNamespace: openshift-pipelines
  addon:
    params:
    - name: clusterTasks
      value: "true"
    - name: pipelineTemplates
      value: "true"
...
```

|     | As a cluster administrator or an user with appropriate privileges, when you disable the automatic creation of RBAC resources for all namespaces, the default `ClusterTask` resource does not work. For the `ClusterTask` resource to function, you must create the RBAC resources manually for each intended namespace. |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
