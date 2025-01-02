# Ansible dynamic inventory
 
Ansible's dynamic inventory feature allows you to use real-time data from external sources to define which hosts Ansible should manage, rather than using statically defined lists of hosts in a typical inventory file. This is particularly useful in environments where your infrastructure is changing frequently, such as cloud environments with instances being spun up and down regularly.

### Example with AWS EC2

- For AWS EC2, you can use the aws_ec2 plugin, which is part of Ansible's default set of plugins. Here’s how to set it up.
  Create a YAML configuration file for the plugin. For example, 

```
### aws_ec2.yaml ###
plugin: amazon.aws.aws_ec2
regions:
  - us-east-1
  - us-west-1
include_filters:
  - tag:Name:
      - 'my_first_tag'
  - tag:Name:
      - 'my_second_tag'
```

- Enable the Plugin

```
### ansible.cfg ###
[inventory]
enable_plugins = aws_ec2
```

- Execute Ansible Commands

```
ansible -i aws_ec2.yaml -m ping all
```
