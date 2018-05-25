# openshift-project-cleaner

### Cleanup OpenShift projects

Deletes all non-crucial OpenShift cluster projects, by 
1) logging in to what should be a system:admin or cluster-admin user
2) gets list of projects and filters out the important ones
> specifically: openshift-infra, openshift-node, openshift, logging, kube-system, kube-service-catalog, kube-public, openshift-template-service-broker, default, management-infra, openshift-ansible-service-broker, dashai
3) outputs the projects to be deleted to ansible debug output
4) deletes said projects

This is useful for cleaning up lab environments or anywhere that the non-core projects need to be cleared away.

Be aware that while this playbook isn't built to be purely idempotent, if there are no extraneous groups in the cluster, then the delete step fails, as there are no namespaces to delete.

### HOW TO USE:

0) git clone this repo to your ansible master

1) setup the hosts.inv inventory file with a single master IP address and the remote username for ansible-ssh-ing.

Note That this playbook assumes the remote user has a kube/config in place so that the remote user gets system:admin.

2) run the playbook from an ansible master and watch it complete.

`ansible-playbook -i hosts.inv clean.yml`
