A script that extracts as much information as possible from an TripleO stack
----------------------------------------------------------------------------

Example:

```shell
[stack@undercloud ~]$ ./tripleo-stack-dump
[stack@undercloud ~]$ jq .stacks.overcloud.outputs.parameters.NeutronNetworkType result.json
"[u'vxlan']"
```
