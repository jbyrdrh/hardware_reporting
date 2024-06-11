**Hardware Reporting**

This demo shows you how you can take an empty hardware report template file, `hwreport.empty`, on `controlnode`, copy the file to the managed nodes as `hwreport.txt`, and then populate it with the appropriate ansible facts.
The playbook also applies a default `NONE` value if disk names do not exist on a given virtual machine that are defined in `hwreport.empty`.

NOTE: Even though this demo is basic, it is a great building block for learning Ansible and can be combined with other concepts.


