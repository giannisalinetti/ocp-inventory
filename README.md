Role Name
=========

A brief description of the role goes here.
The role **ocp-inventory** generates an OpenShift installation inventory using custom variables.
It can be invoked direectly by bastion hosts before deployment of nodes.

Requirements
------------

Since the role is a simple inventory file generator, no specific requirements are needed.

Role Variables
--------------

The inventory customization is all based on role variables. This is an easier approach than polulating all the
inventory from scratch since most of them are simple booleans that enable/disable features.
Some further tuning of the generated inventory file could be needed after running the playbook.

Example Playbooks
----------------

Including some example of how to use the role for single master or multi master deployments:

    - name: "Single master deployment"
      hosts: localhost
      tasks:
        - name: "Call generator role"
          include_role:
            name: ocp-inventory
          vars:
            generator_inventory_dir: /foo/bar
            generator_masters_list:
              - master1.example.com
            generator_etcd_list:
              - master1.example.com
            generator_nfs_list:
              - master1.example.com
            generator_nodes_map:
              - name: master1.example.com
                labels: ""
              - name: node1.example.com
                labels: "openshift_node_labels=\"{\'region\': \'infra\'}\""
              - name: node2.example.com
                labels: "openshift_node_labels=\"{\'region\': \'primary\'}\""


    - name: "Multi master deployment"
      hosts: localhost
      tasks:
        - name: "Call generator role"
          include_role:
            name: ocp-inventory
          vars:
            generator_inventory_dir: /foo/bar
            generator_install_version: v3.9
            generator_multi_master: True
            generator_multi_infra: True
            generator_infra_replicas: 3
            generator_haproxy_enabled: False
            generator_cluster_hostname: testocp.example.com
            generator_cluster_public_hostname: ocpapi.example.com
            generator_ext_dns_wildcard: ocpapps.example.com
            generator_masters_list:
              - master1.example.com
              - master2.example.com
              - master3.example.com
            generator_etcd_list:
              - master1.example.com
              - master2.example.com
              - master3.example.com
            generator_nfs_list:
              - master1.example.com
            generator_nodes_map:
              - name: master1.example.com
                labels: ""
              - name: master2.example.com
                labels: ""
              - name: master3.example.com
                labels: ""
              - name: node1.example.com
                labels: "openshift_node_labels=\"{\'region\': \'infra\'}\""
              - name: node2.example.com
                labels: "openshift_node_labels=\"{\'region\': \'infra\'}\""
              - name: node3.example.com
                labels: "openshift_node_labels=\"{\'region\': \'infra\'}\""
              - name: node4.example.com
                labels: "openshift_node_labels=\"{\'region\': \'primary\'}\""

TODO
----

Add GlusterFS support.
Add External NFS storage support.
Add Cinder Volumes support.
Add VMWare storage support.

License
-------

GPLv3

Author Information
------------------

Gianni Salinetti
