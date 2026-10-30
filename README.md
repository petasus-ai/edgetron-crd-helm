# edgetron-crd-helm (moved)

edgetron's CustomResourceDefinitions now live in the edgetron chart itself, in
[PETASUS/edgetron](https://gitlab.tde.sktelecom.com/PETASUS/edgetron) under
`deployment/edgetron/templates/crd`: they are installed with the release `edgetron`, and
published with the chart from that repository's pipeline, X.Y.Z with each edgetron release
vX.Y.Z and 0.0.0-dev from its main branch, to
[petasus-ai/edgestack-helm](https://github.com/petasus-ai/edgestack-helm). Each carries
`helm.sh/resource-policy: keep`, so uninstalling edgetron leaves them.

A hub that has the release `edgetron-crd` keeps its CRDs, and every object of their
kinds, when edgespray upgrades edgetron to a chart that carries them: it forgets the old
release (its Helm release Secrets) and marks the CRDs as the `edgetron` release's, which
the upgrade adopts. Never `helm uninstall edgetron-crd`: this chart's CRDs lack the keep
policy, so it deletes the CRDs and every object of their kinds.

The edgetron charts up to 3.5.0-rc.3, and the interim edgetron 3.5.0 that its v3.5.0
release replaces, do not carry the CRDs, so they keep using this chart's 3.5.0, released
from this repository's `release-3.5` branch; from 3.5.0-rc.4 edgetron carries them
itself. Nothing is published from `main` any more.
