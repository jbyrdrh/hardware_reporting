**Hardware Reporting with Ansible**

**In this post:**
- This demo shows you how you can take an empty hardware report template file, `hwreport.empty`, on `controlnode`, copy the file to the managed nodes as `hwreport.txt`, and then populate it with the appropriate ansible facts.
- The playbook also applies a default `NONE` value if disk names do not exist on a given virtual machine that are defined in `hwreport.empty`.

NOTE: Even though this demo is basic, it is a great building block for learning Ansible and can be combined with other concepts.

**Environment overview**

In my example environment, I have a control node system named `controlnode` running RHEL 9.4 and six managed nodes: `rhel9-server1`, `rhel9-server2`, `rhel9server3`, and `rhel9server4', all running RHEL 9.4, and `rhel8-server1` and `rhel8-server2`, both running RHEL 8.10.

**Cloning the GitHub Demo Repository**

*NOTE: The files provided in this repo are tailored specifically for my Red Hat test environment. It is important to note that you will need to modify hostnames, filenames, network references, etc. as appropriate for your test environment.*

I recommend [adding your controlnode SSH key to GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account?tool=webui) in order to clone the repository.

- Once the SSH key has been added and GitHub is configured on `controlnode` with your [email address](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/setting-your-commit-email-address) and [username](https://docs.github.com/en/get-started/getting-started-with-git/setting-your-username-in-git), then clone the reposistory in the following manner:
~~~
[jbyrd@controlnode]$ git clone https://github.com/jbyrdrh/hardware_reporting
Cloning into 'hardware_reporting'...
...
~~~


**The ansible.cfg and inventory files**

~~~
[defaults]
inventory= ./inventory

[privilege_escalation]
become=True
become_method=sudo
become_user=root
become_ask_pass=False
~~~

- The `inventory` file for this demo is as follows:
~~~
[rhel9]
rhel9-server1
rhel9-server2
rhel9-server3
rhel9-server4

[rhel8]
rhel8-server1
rhel8-server2
~~~

