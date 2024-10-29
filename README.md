# REPRODUCER

```
oc new-project buildah-issue-5786
```
```
oc get secret etc-pki-entitlement -n openshift-config-managed -o json | jq 'del(.metadata.creationTimestamp, .metadata.resourceVersion, .metadata.resourceVersion, .metadata.namespace, .metadata.uid)' | oc create -f -
```
```
curl -sk https://raw.githubusercontent.com/gmeghnag/buildah-issue-5786/refs/heads/main/buildah-pod-working.yaml | oc create -f -
```
```
curl -sk https://raw.githubusercontent.com/gmeghnag/buildah-issue-5786/refs/heads/main/buildah-pod-not-working.yaml | oc create -f -
```
