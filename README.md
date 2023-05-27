# Ansible playbook to provision Microshift ISO

- Add your VM host relevant information into inventory file. **sudo** privilege must be enabled for the user running the automation. Since we are running in an Execution Environment, ensure you are able to SSH to the VM Host before you start.
- The default kickstart (present as a template in *templates* folder) configures user **admin** (password: redhat)
- Configure your OCP Pull Secret in the **builder-config.yml** file. The pull secret for Red Hat images that can be obtained here [https://console.redhat.com/openshift/install/pull-secret](https://console.redhat.com/openshift/install/pull-secret)

# Build your execution environment

Under execution-environment folder all the files for building the EE are present.

    ansible-builder build  -t r4e-ee

# Run the playbook

The image name is already configured in **ansible-navigator.yaml** file

To run the automation:

    ansible-navigator ansible-navigator run 01_prepare_builder_node.yml -m stdout

