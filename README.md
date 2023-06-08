
Graylog Ansible Role


Example Playbook
Here is an example playbook that uses this role. This is a single-instance configuration. It installs Java, MongoDB, Elasticsearch, and Graylog onto the same server.

```

- hosts: all
  become: true
  vars:
    #Elasticsearch vars
    es_major_version: "7.x"
    es_version: "7.10.2"
    es_enable_xpack: False
    es_instance_name: "graylog"
    es_heap_size: "1g"
    es_config:
      node.name: "graylog"
      cluster.name: "graylog"
      http.port: 9200
      transport.tcp.port: 9300
      network.host: "127.0.0.1"
      discovery.seed_hosts: "localhost:9300"
      cluster.initial_master_nodes: "graylog"
    oss_version: True
    es_action_auto_create_index: False

    #Graylog vars
    graylog_version: 5.1
    graylog_install_java: True
    graylog_password_secret: "Your secret password"
    graylog_root_password_sha2: "Your sha2 password"
    graylog_http_bind_address: "{{ ansible_default_ipv4.address }}:9000"
    graylog_http_publish_uri: "http://{{ ansible_default_ipv4.address }}:9000/"
    graylog_http_external_uri: "http://{{ ansible_default_ipv4.address }}:9000/"

  roles:
    - role: "emirdezem.graylog"
      tags:
        - "graylog"

        

```
