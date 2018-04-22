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

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

---
    - name: "Test inventory generator"
      hosts: localhost
      tasks:
        - name: "Call generator role"
          include_role:
            name: ocp-inventory
          vars:
            generator_inventory_dir: /tmp
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

License
-------

GPLv3

Author Information
------------------

Gianni Salinetti
