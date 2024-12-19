# Gitea Helm Chart for Validated Patterns

This is a small fork to make sure that gitea runs on openshift, that it uses
the more simple non-ha postgresql backend and that a route is exposed by
default.

The upstream repo is at https://gitea.com/gitea/helm-chart

## Why

The reason for forking it and not having a full subchart + override in
top-level values.yaml is the number of bugs helm has when trying to remove
subkeys from subcharts (or in the case of gitea as a subchart: subsubcharts).
Or general issues with subcharts.

See:

* https://www.github.com/helm/helm/issues/12511
* https://www.github.com/helm/helm/issues/12599
* https://www.github.com/helm/helm/issues/12677
* https://www.github.com/helm/helm/issues/12730
* https://www.github.com/helm/helm/issues/12488
* https://www.github.com/helm/helm/issues/12741

By doing this we do not need to patch values files in subcharts and
dependencies of subcharts

## Update this chart

1. Rebase from the upstream repo at https://gitea.com/gitea/helm-chart and fix any conflicts
2. Update the version in Chart.yaml
3. Build a test helm package via `helm package .` (this will create a "gitea-0.0.x.tgz" file)
4. Create index.yaml with your custom url via `helm repo index --url https://foo.org/files/helm-repo .`
5. Copy index.yaml, subcharts and helm package to your web server `scp -rp index.yaml charts gitea-0.0.3.tgz foo:/srv/foo.org/files/helm-repo`
6. Deploy a pattern by setting the needed vars in `values-global.yaml`:
   ```
   main:
     clusterGroupName: datacenter
     multiSourceConfig:
       enabled: true
       clusterGroupChartVersion: 0.9.*
     git:
       repoUpstreamURL: https://github.com/mbaldessari/industrial-edge
     gitea:
       chartVersion: 0.0.3
       chartName: gitea
       helmRepoUrl: https://foo.org/files/helm-repo
   ```