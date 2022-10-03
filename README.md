## Repositories

A chart repository is a web server that houses packaged charts which can be discovered and shared. A chart repository includes an `index.html` file that contains information about each chart in a repository.

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

Package a chart directory into a chart archive (creates a `tgz` file).

The name of the archived chart is derived from the `name` property in the Chart.yaml file.

`helm package [PATH]`

A chart can be packaged and written to a specified local destination.

`helm package [PATH] -d [DESTINATION STRING]`

#### .helmignore

The .helmignore file is used to specify files that should not be packaged with a chart.
