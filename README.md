# What is Helm?

Helm is a package managher for Kubernetes. Helm helps you manage Kubernetes applications — Helm charts help you define, install, and upgrade even the most complex Kubernetes application.


## Terminology and Concepts

#### Chart

A chart is a Helm package and collection of YAML files that describe Kubernetes resources. It contains all the configuration to run an application or service.

#### Starters

Helm starters are used by the `helm create` command to customize the default chart — by default Helm uses an NGINX chart as the default chart.

As chart author you may author charts that are specifically designed to be used as starters.

#### Manifest

A manifest is a YAML-encoded representation of the Kubernetes resources that were generated from a release's chart.

#### Release

A release is an instance of a Helm chart running in a cluster. Installing a chart into a cluster will create a release.

#### Dependencies

Helm chart dependencies are used to install other charts’ resources that a Helm chart may depend on. Helm charts store their dependencies in 'charts/'. For chart developers, it is often easier to manage dependencies in 'Chart.yaml' which declares all dependencies.

The dependency commands operate on that file, making it easy to synchronize between the desired dependencies and the actual dependencies stored in the 'charts/' directory.

## Helm Commands

#### helm list

Lists all of the releases for a specified namespace (uses current namespace context if namespace not specified).

`helm list`

Example: `helm list -n foo`

#### helm install

Install a package (Helm chart).

`helm install [RELEASE NAME] [REPOSITORY NAME]/[CHART NAME]`

`helm install [RELEASE NAME] [PATH TO CHART DIRECTORY]`

`helm install [RELEASE NAME] .` Command when executing from within the chart directory

To override values in a chart, use either the '--values' flag and pass in a file or use the '--set' flag and pass configuration from the command line.

##### --generate-name

Autogenerate the name (and omit the NAME parameter).

##### --wait

Wait until the release is in a ready state before marking the release as successful.

##### --atomic

Delete the installation and rollback on failure. Useful for continuous integration and continuous deployment.

##### --dry-run

Simulate an install. Load the chart, parse 'values.yaml', generate manifest and parse YAML Kubernetes object for validation. Does not send Kubernetes objects to Kubernetes. Useful for debugging manifests.

#### helm get manifest

Fetches the generated manifest for a given release at the time of deployment.

`helm get manifest [RELEASE NAME]`

`kubectl` can be used to fetch what is in Kubernetes at the present time.

Example: `kubectl get deployments [DEPLOYMENT NAME] -o yaml`

#### helm get values

Fetches the values for a given release at the time of deployment.

`helm get values [RELEASE NAME]`

#### helm create

Create a new chart with a specified name (creates an NGINX chart by default).

`helm create [CHART NAME]`

##### --starter

Option that lets you specify a starter chart.

`helm create --starter [NAME OF STARTER] [NAME OF CHART]`

Starter charts should be stored in a specific local directory.

Run `helm env HELM_DATA_HOME` to return the directory to store starter charts.

Starter charts should be designed with the following considerations in mind:

* The 'Chart.yaml' will be overwritten by the generator and specified chart name. The `name` property in 'Chart.yaml' file does not need to be parameterized. It will be overrriden when executing the `helm create` command.
* Users will expect to modify such a chart's contents, so documentation should indicate how users can do so.
* All occurrences of <CHARTNAME> will be replaced with the specified chart name so that starter charts can be used as templates.

#### helm lint

`helm template [PATH TO CHART DIRECTORY]`

Runs a series of tests to verify that the chart is well-formed. Examine a chart for possible issues.

#### helm template

Locally render template. Does not send Kubernetes objects to Kubernetes or parse for validation. Useful for reviewing template and debugging syntatical errors.

`helm template [PATH TO CHART DIRECTORY]`

#### helm dependency update

Update `charts/` based on the contents of `Chart.yaml`.

`helm dependency update [PATH TO CHART DIRECTORY]`

The command autogenerates a lock file lists the exact versions of immediate dependencies and their dependencies and their dependencies.

#### helm upgrade

Upgrade a release with a new version of a chart.

`helm upgrade [RELEASE NAME]'

##### --install

If a release by this name doesn't already exist, install first. Useful for continuous integration and continuous deployment as a package will first be installed.

##### --cleanup-on-failure

Delete new resources created in this upgrade when upgrade fails. Can hinder debugging when an upgrade fails.

#### helm uninstall

`helm uninstall [RELEASE NAME]'

##### --keep-history

Remove all associated resources and mark the release as deleted, but retain the release history.

## Repositories

A chart repository is a web server that houses packaged charts which can be discovered and shared. A chart repository includes an 'index.html' file that contains information about each chart in a repository.

#### helm repo add

Add and store a chart repository locally.

`helm repo add [NAME] [URL]`

Example: `helm repo add bitnami https://charts.bitnami.com/bitnami`

#### helm repo list

List locally stored charts.

`helm repo list`

#### helm repo remove

Remove a locally stored chart repository.

`helm repo remove [NAME]`

Example: `helm repo remove bitnami`

#### helm repo update

Get and update the locally stored chart repositories from their respective remote chart repository.

`helm repo update`

#### helm pull

Download a specified chart from a repository.

`helm pull [URL]/[NAME]`

#### helm package

Package a chart directory into a chart archive (creates a 'tgz' file).

The name of the archived chart is derived from the `name` property in the 'Chart.yaml' file.

`helm package [PATH]`

A chart can be packaged and written to a specified local destination.

`helm package [PATH] -d [DESTINATION STRING]`

#### .helmignore

The '.helmignore' file is used to specify files that should not be packaged with a chart.
