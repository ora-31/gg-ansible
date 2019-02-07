# gg-ansible
Oracle GoldenGate replication with Ansible

When migrating data from your own data center to a public or private cloud, a key success factor is 100% data integrity between the source and the target database at all times. Some of your applications may only allow for limited downtime when the switch to a cloud database occurs. The strategy we deployed for our migrations was based on using Oracle GoldenGate to replicate data in real time from the on-premises database to the cloud database, automating the entire process. This Ansible Playbook and associated configuration files will help you achieve the same results.

**Note:** You will have to modify all configuration files to reflect your own environment. I'm available to answer any questions, simply email me at scome98 at gmail

**Command Line Example:** Here is an example of the command line used to setup a replication between a source and target instance"
`./gg_stream.yml -i /etc/ansible/oracle_hosts --limit "sandbox" --extra-vars "stream=SC source=cogcss target=tqbirt debug_mode=true remap_tablespace=USERS:USERS destroy=True"`

**Parameters Explained**
`-i inventory_file` An inventory file containing all your source and target hosts (physical hostnames) and groups of hosts
`--limit "group"` Create a group containing the source and target hosts only
`extra--vars "name=value,"` A list of name/value pairs used to provide dynamic parameters explained below:

**extra-vars**
`stream` Defines the actual stream you want to setup. Streams are defined in the vars/streams.yml file. A stream defines the name of the extract. pump and replicat processes, and also the name of the schema to include (one or many) in the replication.
`source` The Oracle source instance name running on the source host
`target` The Oracle target instance name running on the target host
`debug_mode` When set to True, the various scripts generated will not be deleted. Use this if you want the scripts generated and kept for debugging purposes.
`destroy` When set to True, this will remove the matching existing streams as well as drop all objects in the target schema. Make sure to test this on your sandbox systems before running it in production as you may loose data.
`remap_tablespace` Use this parameter for the import data pump in order to remap tablespaces if different between the source and target.
