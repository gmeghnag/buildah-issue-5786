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


# FAILING POD OUTPUT
Error message from failing pod `buildah-issue-5786-1-32-2-not-working`:
```
$ oc logs pod/buildah-issue-5786-1-32-2-not-working | tail -50
time="2024-10-29T13:55:57Z" level=debug msg="bind mounted \"/var/tmp/buildah3386043866/hosts\" to \"/var/tmp/buildah3386043866/mnt/rootfs/etc/hosts\""
time="2024-10-29T13:55:57Z" level=debug msg="bind mounting \"/etc/resolv.conf\" on \"/var/tmp/buildah3386043866/mnt/rootfs/etc/resolv.conf\" [rbind]"
time="2024-10-29T13:55:57Z" level=debug msg="bind mounted \"/var/tmp/buildah3386043866/resolv.conf\" to \"/var/tmp/buildah3386043866/mnt/rootfs/etc/resolv.conf\""
time="2024-10-29T13:55:57Z" level=debug msg="bind mounting \"/run/.containerenv\" on \"/var/tmp/buildah3386043866/mnt/rootfs/run/.containerenv\" [rbind]"
time="2024-10-29T13:55:57Z" level=debug msg="bind mounted \"/var/tmp/buildah3386043866/run/.containerenv\" to \"/var/tmp/buildah3386043866/mnt/rootfs/run/.containerenv\""
time="2024-10-29T13:55:57Z" level=debug msg="bind mounting \"/etc/pki/entitlement/\" on \"/var/tmp/buildah3386043866/mnt/rootfs/etc/pki/entitlement\" [ rw private rbind]"
time="2024-10-29T13:55:57Z" level=debug msg="bind mounted \"/var/tmp/buildah3386043866/mnt/buildah-bind-target-10\" to \"/var/tmp/buildah3386043866/mnt/rootfs/etc/pki/entitlement\""
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/buildah-bind-target-11\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/buildah-bind-target-10\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=warning msg="pkg/bind: error detaching \"/var/tmp/buildah3386043866/mnt/buildah-bind-target-10\": permission denied"
time="2024-10-29T13:55:57Z" level=warning msg="pkg/bind: error removing \"/var/tmp/buildah3386043866/mnt/buildah-bind-target-10\": device or resource busy"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/sys/firmware\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/sys/fs/cgroup\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/sys/firmware\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/sys/fs/cgroup\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/sys\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/sys/firmware\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/sys/fs/cgroup\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/proc/scsi\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/proc/timer_list\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/proc/keys\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/proc/kcore\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/proc/acpi\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/proc/sysrq-trigger\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/proc/sys\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/proc/irq\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/proc/fs\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/proc/bus\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/dev/termination-log\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/dev/shm\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/dev/mqueue\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/dev/pts\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/etc/pki/entitlement\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/run/.containerenv\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/etc/resolv.conf\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/etc/hosts\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/etc/hostname\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/sys\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/proc\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs/dev\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/rootfs\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt/buildah-bind-target-10\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=debug msg="\"/var/tmp/buildah3386043866/mnt\" is apparently not really mounted, skipping"
time="2024-10-29T13:55:57Z" level=warning msg="pkg/bind: error removing \"/var/tmp/buildah3386043866/mnt\": directory not empty"
time="2024-10-29T13:55:57Z" level=debug msg="error cleaning up intermediate mount NS: remounting \"/var/tmp/buildah3386043866/mnt/rootfs/etc/pki/entitlement\" in mount namespace with flags 0x0 instead of 0x1: permission denied"
error running subprocess: remounting "/var/tmp/buildah3386043866/mnt/rootfs/etc/pki/entitlement" in mount namespace with flags 0x0 instead of 0x1: permission denied
time="2024-10-29T13:55:58Z" level=debug msg="Error building at step {Env:[GIT_REVISION=updateme APP_VERSION=updateme QUAY_TAG_EXPIRATION=180d PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin container=oci LANG=en_US.UTF-8 LANGUAGE=en_US:en LC_ALL=en_US.UTF-8 TZ=UTC] Command:run Args:[set -ex &&   sed -i 's/^LANG=.*/LANG=\"en_US.utf8\"/' /etc/locale.conf &&   ln -fvs /usr/share/zoneinfo/America/New_York /etc/localtime &&   PKGMGR='microdnf' &&   BUILDTIME_PKGS=\"\" &&   RUNTIME_PKGS=\"glibc-langpack-en nss_wrapper uid_wrapper\" &&   ls -lah /etc/pki/entitlement &&   ${PKGMGR}   --enablerepo=\"ubi-9-appstream-rpms\"   --enablerepo=\"ubi-9-baseos-rpms\"   --enablerepo=\"ubi-9-codeready-builder-rpms\"   --enablerepo=\"rhel-9-for-x86_64-baseos-rpms\"   --enablerepo=\"rhel-9-for-x86_64-appstream-rpms\"   --enablerepo=\"codeready-builder-for-rhel-9-x86_64-rpms\"   install --nodocs --best --assumeyes --setopt=tsflags=nodocs --setopt=install_weak_deps=0   ${BUILDTIME_PKGS} ${RUNTIME_PKGS}] Flags:[] Attrs:map[] Message:RUN set -ex &&   sed -i 's/^LANG=.*/LANG=\"en_US.utf8\"/' /etc/locale.conf &&   ln -fvs /usr/share/zoneinfo/America/New_York /etc/localtime &&   PKGMGR='microdnf' &&   BUILDTIME_PKGS=\"\" &&   RUNTIME_PKGS=\"glibc-langpack-en nss_wrapper uid_wrapper\" &&   ls -lah /etc/pki/entitlement &&   ${PKGMGR}   --enablerepo=\"ubi-9-appstream-rpms\"   --enablerepo=\"ubi-9-baseos-rpms\"   --enablerepo=\"ubi-9-codeready-builder-rpms\"   --enablerepo=\"rhel-9-for-x86_64-baseos-rpms\"   --enablerepo=\"rhel-9-for-x86_64-appstream-rpms\"   --enablerepo=\"codeready-builder-for-rhel-9-x86_64-rpms\"   install --nodocs --best --assumeyes --setopt=tsflags=nodocs --setopt=install_weak_deps=0   ${BUILDTIME_PKGS} ${RUNTIME_PKGS} Original:RUN set -ex &&   sed -i 's/^LANG=.*/LANG=\"en_US.utf8\"/' /etc/locale.conf &&   ln -fvs /usr/share/zoneinfo/America/New_York /etc/localtime &&   PKGMGR='microdnf' &&   BUILDTIME_PKGS=\"\" &&   RUNTIME_PKGS=\"glibc-langpack-en nss_wrapper uid_wrapper\" &&   ls -lah /etc/pki/entitlement &&   ${PKGMGR}   --enablerepo=\"ubi-9-appstream-rpms\"   --enablerepo=\"ubi-9-baseos-rpms\"   --enablerepo=\"ubi-9-codeready-builder-rpms\"   --enablerepo=\"rhel-9-for-x86_64-baseos-rpms\"   --enablerepo=\"rhel-9-for-x86_64-appstream-rpms\"   --enablerepo=\"codeready-builder-for-rhel-9-x86_64-rpms\"   install --nodocs --best --assumeyes --setopt=tsflags=nodocs --setopt=install_weak_deps=0   ${BUILDTIME_PKGS} ${RUNTIME_PKGS}}: exit status 1"
Error: building at STEP "RUN set -ex &&   sed -i 's/^LANG=.*/LANG="en_US.utf8"/' /etc/locale.conf &&   ln -fvs /usr/share/zoneinfo/America/New_York /etc/localtime &&   PKGMGR='microdnf' &&   BUILDTIME_PKGS="" &&   RUNTIME_PKGS="glibc-langpack-en nss_wrapper uid_wrapper" &&   ls -lah /etc/pki/entitlement &&   ${PKGMGR}   --enablerepo="ubi-9-appstream-rpms"   --enablerepo="ubi-9-baseos-rpms"   --enablerepo="ubi-9-codeready-builder-rpms"   --enablerepo="rhel-9-for-x86_64-baseos-rpms"   --enablerepo="rhel-9-for-x86_64-appstream-rpms"   --enablerepo="codeready-builder-for-rhel-9-x86_64-rpms"   install --nodocs --best --assumeyes --setopt=tsflags=nodocs --setopt=install_weak_deps=0   ${BUILDTIME_PKGS} ${RUNTIME_PKGS}": exit status 1
time="2024-10-29T13:55:58Z" level=debug msg="shutting down the store"
time="2024-10-29T13:55:58Z" level=debug msg="exit status 1"
```
