# Collection of scripts to do post-deployment analyse of a TripleO deployment

## tripleo-stack-dump

Extract as much details as possible from a running stack. The final output is a JSON file. This can be used
to investigate a stack deployment failure of list the parameters used during the creation.

Example:

```shell
[stack@undercloud ~]$ ./tripleo-stack-dump
[stack@undercloud ~]$ jq .stacks.overcloud.outputs.parameters.NeutronNetworkType tripleo-stack-dump.json
"[u'vxlan']"
```

## list_nodes_status

Loop on each nodes of the cluster and:

- ensure the SSH connection from the undercloud works
- show up the last os-collect-config error found on the node 

```shell
[stack@directorvm tripleo-stack-dump]$ ./list_nodes_status 
+--------------------------------------+--------------------------+--------+------------+-------------+-------------------------+
| ID                                   | Name                     | Status | Task State | Power State | Networks                |
+--------------------------------------+--------------------------+--------+------------+-------------+-------------------------+
| 8c325196-f73d-4207-8f4a-5e8b616dff62 | 716182-lab2-controller01 | ACTIVE | -          | Running     | ctlplane=172.22.216.113 |
| 793efb82-2651-4ba1-bd96-f48bceabaa13 | 716183-lab2-controller02 | ACTIVE | -          | Running     | ctlplane=172.22.216.112 |
| 876e755c-861a-43d4-8fd3-cd815dd6b191 | 716184-lab2-controller03 | ACTIVE | -          | Running     | ctlplane=172.22.216.114 |
| 62436466-9118-49b5-823b-a569983cae3f | 716185-lab2-compute01    | ACTIVE | -          | Running     | ctlplane=172.22.216.110 |
| bf8a8a9b-2d4b-4a3e-ae89-49f896fba0e1 | 716186-lab2-compute02    | ACTIVE | -          | Running     | ctlplane=172.22.216.109 |
| d26b9e4e-d0ab-4b3b-aebe-d52d7071f2d3 | 716187-lab2-compute03    | ACTIVE | -          | Running     | ctlplane=172.22.216.111 |
| 98a1e50c-b542-457d-b05a-3aacc7596b5b | 716199-lab2-cephperf01   | ACTIVE | -          | Running     | ctlplane=172.22.216.107 |
| 117ad7bf-372a-4291-9273-59550da735b3 | 716200-lab2-cephperf02   | ERROR  | -          | NOSTATE     |                         |
| 09b18750-e1e6-4575-9eda-ccad166ec0b9 | 716201-lab2-cephcap01    | ACTIVE | -          | Running     | ctlplane=172.22.216.108 |
+--------------------------------------+--------------------------+--------+------------+-------------+-------------------------+
** 172.22.216.113 up and running
Error: /usr/sbin/rabbitmqctl add_user maas key_maas_pass returned 2 instead of one of [0]
** 172.22.216.112 up and running
** 172.22.216.114 up and running
** 172.22.216.110 up and running
** 172.22.216.109 up and running
** 172.22.216.111 up and running
** 172.22.216.107 up and running
** 172.22.216.108 up and running
```
