# VP gitea-chart

## Updating the chart

1. Edit Chart.yaml with the new version
2. In the gitea-chart folder, run: `helm dependency update .`
3. Run `./update-helm-dependency.sh`
4. Git add the new chart in `./charts/vault-<version>.tgz`

## Patches

