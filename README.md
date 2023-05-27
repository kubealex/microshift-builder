# Ansible playbook to provision rhel4edge vms and register into and ACM hub

## Important steps

- Python >= 3.8 must be installed on the machine running this tool

- RHEL4EDGE ISO should be built prior to running the too and placed in *rhel4edge* folder **(image name: r4e-microshift-installer.x86_64.iso)**

- Populate vars.yml file with relevant information. Please respect the format.
 
        github_repo: #if you delete this variable, it defaults to microshift-config
        github_username: #i.e. kubealex
        github_token: # your github token 

        rhel4edge_instances: 
        - cluster_name: r4e-printer
          cluster_role: printer
        - cluster_name: r4e-injection 
          cluster_role: injection
        - cluster_name: r4e-label
          cluster_role: label

*rhel4edge_instances* will hold the values for the **cluster name**, that will be used both for the hostname and the name of the microshift instance, and the **cluster role** of the instance, for enforcing placement rules.

- Add your VM host relevant information into inventory file. **sudo** privilege must be enabled for the user running the automation. Since we are running in an Execution Environment, ensure you are able to SSH to the VM Host before you start. 
- The default kickstart (present as a template in *templates* folder) uses the id_rsa.pub key in the repo for user **redhat** (password: redhat)
- Files to be placed in the **root** folder of this repo:
*pullSecret* - The pull secret for Red Hat images that can be obtained here [https://console.redhat.com/openshift/install/pull-secret](https://console.redhat.com/openshift/install/pull-secret)
*kubeconfig* - The kubeconfig of the cluster running RHACM

# Build your execution environment

Under execution-environment folder all the files for building the EE are present.

    ansible-builder build  -t r4e-ee

# Run the playbook 

The image name is already configured in **ansible-navigator.yaml** file

To run the automation:

    ansible-navigator ansible-navigator run 02_vms-and-registration -m stdout 

