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
