  <picture>
    <source width="200" media="(prefers-color-scheme: dark)" srcset="https://www.vectorlogo.zone/logos/ansible/ansible-ar21.png">
    <img width="200" src="https://www.vectorlogo.zone/logos/ansible/ansible-ar21.png">
  </picture>
  
## Ansible cheat sheet

 
| Category | Command/Option | Explanation |
|---|---|---|
| General | `ansible --version` | Display the version of Ansible installed. |
| General | `ansible -m ping all` | Ping all hosts to check if they are reachable. |
| General | `ansible -m shell -a 'free -m' all` | Run the 'free -m' shell command on all hosts. |
|---|---|---|
| Playbooks | `ansible-playbook playbook.yml` | Run the playbook named `playbook.yml`. |
| Playbooks | `ansible-playbook -i inventory.ini playbook.yml` | Run a playbook with a specified inventory file. |
| Playbooks | `ansible-playbook playbook.yml --syntax-check` | Perform a syntax check on the playbook. |
| Playbooks | `ansible-playbook playbook.yml --start-at-task='taskname'` | Start the playbook at the specified task. |
| Playbooks | `ansible-playbook playbook.yml --list-hosts` | List all hosts the playbook will run against. |
| Playbooks | `ansible-playbook playbook.yml --list-tasks` | List all tasks the playbook will execute. |
| Playbooks | `ansible-playbook playbook.yml --step` | Execute the playbook interactively, asking for confirmation at each step. |
| Playbooks | `ansible-playbook playbook.yml --check` | Do a dry run of the playbook without making actual changes. |
| Playbooks | `ansible-playbook playbook.yml --diff` | Show differences in files when running the playbook. |
| Playbooks | `ansible-playbook playbook.yml --tags "tag1,tag2"` | Run only the tasks tagged with tag1 and tag2. |
| Playbooks | `ansible-playbook playbook.yml --skip-tags "tag3"` | Skip tasks tagged with tag3. |
| Playbooks | `ansible-playbook playbook.yml --limit servers` | Limit the playbook execution to the group 'servers'. |
| Playbooks | `ansible-playbook playbook.yml --extra-vars "version=1.2.3"` | Run the playbook with extra variables. |
| Playbooks | `ansible-playbook playbook.yml --forks=5` | Set the number of parallel processes to 5. |
| Playbooks | `ansible-playbook playbook.yml -v` | Run the playbook in verbose mode. `-vvv` and `-vvvv` can be used for more verbosity. |
| Playbooks | `ansible-playbook playbook.yml --check --diff` | Dry-run the playbook and show file differences. |
|---|---|---|
| Roles | `ansible-galaxy init role_name` | Initialize a new role structure with the specified name. |
| Roles | `ansible-galaxy install role_name` | Install an Ansible role. |
|---|---|---|
| Vault | `ansible-vault create vault.yml` | Create a new encrypted file. |
| Vault | `ansible-vault view vault.yml` | View an encrypted file. |
| Vault | `ansible-vault edit vault.yml` | Edit an encrypted file. |
| Vault | `ansible-vault decrypt vault.yml` | Decrypt an encrypted file. |
| Vault | `ansible-vault encrypt vault.yml` | Encrypt a file. |
| Vault | `ansible-vault rekey vault.yml` | Change the password on a vault file. |
| Vault | `ansible-vault encrypt_string --name 'var_name' 'string'` | Encrypt a string and output it in a format ready for use with Ansible. |
| Vault | `ansible-playbook playbook.yml --ask-vault-pass` | Run a playbook and prompt for the vault password. |
| Vault | `ansible-playbook playbook.yml --vault-password-file vault.pass` | Run a playbook using a file containing the vault password. |
| Vault | `ansible-vault encrypt_string --stdin-name 'var_name'` | Read the string from stdin and encrypt it. |
| Vault | `ansible-vault encrypt --vault-id dev@prompt vars.yml` | Encrypt a file using a prompt for the vault password. |
| Vault | `ansible-playbook playbook.yml --vault-id dev@prompt` | Run a playbook using a prompt for the vault password. |
|---|---|---|
| Configuration | `ansible-config list` | List all configuration options. |
| Configuration | `ansible-config dump` | Show the current configuration. |
| Configuration | `ansible-config view` | View the current Ansible configuration. |
| Configuration | `ansible-config dump --only-changed` | Dump configuration items that have changed from the default. |
| Configuration | `ansible-config set ANSIBLE_HOST_KEY_CHECKING=False` | Set a specific configuration item. |
| Configuration | `ansible-config unset ANSIBLE_HOST_KEY_CHECKING` | Unset a specific configuration item. |
|---|---|---|
| Console | `ansible-console` | Start an interactive console for executing Ansible tasks. |
| Console | `ansible-console -i inventory.ini` | Start an interactive console using a specific inventory. |
|---|---|---|
| Modules | `ansible-doc -l` | List available modules. |
| Modules | `ansible-doc module_name` | Get documentation for a specific module. |
|---|---|---|
| Inventory | `ansible-inventory --list -y` | List the inventory in YAML format. |
| Inventory | `ansible-inventory --graph` | Show a graph of the inventory. |
| Inventory | `ansible -i inventory.ini all -m ping` | Use a specific inventory file and ping all hosts. |
| Inventory | `ansible-inventory --host hostname` | Display all variables for a specific host. |
| Inventory | `ansible-inventory --playbook-dir . --graph` | Display a graph of the inventory from the current directory. |
| Inventory | `ansible -i 'localhost,' -c local -m ping` | Ping localhost using local connection and ad-hoc inventory. |
| Inventory | `ansible-inventory --list --yaml` | List inventory in YAML format. |
|---|---|---|
| Pull | `ansible-pull -U git_url` | Pull a Git repository of Ans
| Pull | `ansible-pull -U git_url` | Pull a Git repository of Ansible configurations on the target host. |
|---|---|---|
| Galaxy | `ansible-galaxy collection init my_namespace.my_collection` | Initialize a new collection with the given namespace and name. |
| Galaxy | `ansible-galaxy collection build` | Build an Ansible collection package ready for distribution. |
| Galaxy | `ansible-galaxy collection install my_namespace.my_collection` | Install an Ansible collection from Galaxy. |
| Galaxy | `ansible-galaxy role init my_role` | Initialize a new role with the given name. |
| Galaxy | `ansible-galaxy role install my_role` | Install an Ansible role from Galaxy. |
| Galaxy | `ansible-galaxy list` | List installed roles and collections. |
| Galaxy | `ansible-galaxy collection install -r requirements.yml` | Install collections from a requirements file. |
| Galaxy | `ansible-galaxy role install -r requirements.yml` | Install roles from a requirements file. |
| Galaxy | `ansible-galaxy collection publish ./namespace-collection-1.0.0.tar.gz --api-key=your_token` | Publish a collection to Galaxy using an API token. |
| Galaxy | `ansible-galaxy role init --role-skeleton skeleton my_role` | Initialize a new role with a specified role skeleton. |
|---|---|---|
| Modules | `ansible localhost -m file -a "path=/tmp/test state=touch"` | Create a new file on the local host using the file module. |
| Modules | `ansible localhost -m package -a "name=vim state=present"` | Install a package on the local host using the package module. |
| Modules | `ansible localhost -m command -a "uptime"` | Run a command on the local host using the command module. |
| Modules | `ansible localhost -m user -a "name=testuser state=absent"` | Remove user 'testuser' from the local host using the user module. |
| Modules | `ansible localhost -m service -a "name=httpd state=restarted"` | Restart the 'httpd' service on the local host using the service module. |
| Modules | `ansible localhost -m copy -a "src=/etc/hosts dest=/tmp/hosts"` | Copy '/etc/hosts' to '/tmp/hosts' on the local host using the copy module. |
| Modules | `ansible localhost -m file -a "path=/tmp/test state=absent"` | Remove file '/tmp/test' on the local host using the file module. |
| Modules | `ansible localhost -m apt -a "name=nginx state=latest"` | Install the latest version of 'nginx' on the local host using the apt module (Debian-based systems). |


### How Ansible connect to remote machines
![image](https://user-images.githubusercontent.com/69889600/219846350-a0c53ac4-0b2f-4781-ac6c-a5dd512ea649.png)

**Control machine**: A control machine is the central node in an Ansible infrastructure. It is used to manage all the other machines in the network. 

**Remote machine**: A remote machine is any machine that is not the control machine. Remote machines are managed by the control machine using SSH. 

**Target machine**: A target machine is a remote machine being provisioned or configured by Ansible.


## Ansible directory Structure
```bash	
cd /etc/ansible
ansible.cfg
hosts
roles/
```
___________________________________________________

## Ansible Configuration
- Change the default behaviour of ansible configuration by editing configuration file

#### Order of Ansible Config
- ANSIBLE_CONFIG (set environment variable)
- ansible.cfg (in the current directory)
- ~/.ansible.cfg (in the home directory)
- `/etc/ansible/ansible.cfg` default configuration file

### What is Ansible Config file
- The file that governs the behavior of all interactions performed by the control node. 
- Ansible uses the python module, python script to connect to the target machine. 
- It dumps the python script and execute there and return the output.

```bash
ansible-config list # list all configutation
ansible-config view # Show the current config files
ansible-config dump # show current settings
```

- File content`/etc/ansible/ansible.cfg`
```bash
[defaults]
inventory      = /etc/ansible/hosts

[inventory]

[priviledge_escalation]

[paramiko_connection]

[ssh_connection]

[persistent_connection]

[colors]
```

## INVENTORY (Static) 

### What is Ansible Inventory
- Collection of hosts
- Inventory file defines the hosts and groups of hosts upon which commands, modules, and tasks in a playbook operate. 
- The file can be in one of many formats depending on your Ansible /environment and plugins. 
- The default inventory located at /etc/ansible/hosts
- The **ansible_host** is an invetory parameter which you can use to specify the FQDN or IP address of the server. 

- To set up hosts you need to edit the hosts file in the ansible directory
- You can create seperate  innnventory file. 

```bash
cd /etc/ansible
vi hosts
```
```bash
# You can set up aliases by using the "ansible_host" parameter.
[all]
host_name1   ansible_host=server1.company.com
host_name2   ansible_host=server2.company.com
db1     ansible_host=server3.company.com
db2     ansible_host=server4.company.com

host_name1 ansible_host=private_addr ansible_user=ubuntu ansible_ssh_private_key_file=instance.pem 
host_name2 ansible_host=private_addr ansible_user=ubuntu ansible_ssh_private_key_file=instance.pem 
host_name3 ansible_host=private_addr ansible_user=ubuntu ansible_ssh_private_key_file=instance.pem 

# You can also group the target machines
[web_app]
host_name1
host_name2
[dbserver]
host_name3

# Group of Groups
[AllServers:children]
webserver
dbserver

# Variables at group level
[AllServers:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=instance.pem 
```

___________________________________________________

## Ansible Adhoc Commands
- Ansible provide ad-hoc commands to execute module on target from the shell. 
- When you run ansible commandit create some binery file in python and copy it to client /tmp .ansibe directory.
- Once  done binary get auto deleted from client side.
- Ping will do ssh into Linux machine, if it's succesful it means connection between ansible and hosts are right.
- For particular host use host_name in below command:

### Ansible modules

**ping Module**
```bash
ansible -i inventory -m ping host_name
```
- For all hosts use below commands:
```bash
ansible -i inventory -m ping all
```
```bash
ansible -i inventory -m ping '*'
```
- To find the documentation of the modules
```bash
ansible-doc -l | more
```
```bash
ansible-doc module_name  # To find use of any module
```
```bash
ansible-doc -s yum
```

**setup module**
- Used to get facts while executing Ansible playbook.

```bash
ansible all -m setup
ansible all -m setup -a "filter=ansible_date_time"
```
**shell module**
- To Run any command on the slave machine
```bash
ansible -i hosts <<slave>> -m shell -a 'ls /home'
```

**copy module**
- If file change on client side ansible will rechange the desired state of file.
```bash
ansible [group] -m copy -a "src=source_path dest=destination_path"
ansible [group] -m copy -a "content='Your Content' dest=destination_path_file"
ansible 172.31.27.53 -m copy -a "src=/tmp/testfile dest=/tmp/testfile"   
```

**file module**
- state -->  touch, absent, directory (to create dir)
```bash
ansible [group] -m file -a "path=file/dir_destination_path state=<state>"
ansible [group] -m file -a "path=file/dir_destination_path state=<state> mode=0775"
```

**yum Module**
- state --> present, latest, absent
```bash
ansible [group] -m yum -a "name=httpd state=present"
ansible 172.31.27.53 -m yum -a "name=httpd state=present"

# run as root permission "--become"
ansible 172.31.27.53 -m yum -a "name=httpd state=present" -b
ansible -i inventory -m yum -a "name-httpd state-present" host_name1 --become
```

**service module**
```bash
ansible 172.31.27.53 -m service -a "name=httpd state=started"
```
___________________________________________________

### Ansible Facts (Default Facts)
- Ansible facts are used to get the ansible client information - OS, Processsor, relese, IP etc.
- Task of collecting Ansible Client Information is called the `Gathering Facts` and Gathered information is call the `Facts` or veriables.
- `Setup modules` is used to collect the Facts.
- Playbooks default execute SetUP module to get the information of Ansible Clients. 
___________________________________________________

### Custom Facts (user-define facts)
- Used to get the extra information about your managed nodes.
- If custom Facts are on managed nodes, Then Custom facts will be called default.
- custome facts help to reduce the code lines in playbook
#### Steps to create Custom nodes
1. Create `/etc/ansible/facts.d` on your managed nodes.
2. Inside the `facts.d` create one or morecustom facts file with extension`.fact`
3. Output of the fact file should be `JSON`
4. Fact file should have `execution` permission.

```bash
cd /etc/ansible/facts.d

vi get-facts-ansible-version.facts
#!/bin/bash
ansibe_version=$(ansible --version | grep version | awk '{print $4}')
#printf "$ansibe_version"
# JSON Format
cat << EOF
{
        "ANSIBLE_VERSION": "$ansibe_version"
}
EOF

# Create directory on client /etc/ansible/facts.d
ansible all -m file -a "path=/etc/ansible/facts.d state=directory" -b


# Copy file
ansible all -m copy -a "src=/etc/ansible/facts.d/get-facts-ansible-version.facts dest=/etc/ansible/facts.d" -b

# Make file executable

ansible all -m copy -a "src=/etc/ansible/facts.d/get-facts-ansible-version.fact dest=/etc/ansible/facts.d mode=0770" -b
```
- Done Mistake while giving extension `.fact`

```bash
mv get-facts-ansible-version.facts get-facts-ansible-version.fact

ansible all -m copy -a "src=/etc/ansible/facts.d/get-facts-ansible-version.fact dest=/etc/ansible/facts.d mode=0770" -b
```
- Now checkcustom variable 

```bash
ansible all -m setup -a "filter=ansible_local"
```
___________________________________________________

## INVENTORY (Dynamic)

- Use plugins to get dynamic inventory
- Ansible have Dynamic inventory Script for Public Clouds
- Define inventory to Ansible Command Dynamically.
- In erlier Ansible version, files are present in GitHub. latest version have plugins for inventory file formation.

```bash
# List of Dynamic inventory pugins 
ansible-doc -t inventory -l
```
### AWS dynamic inventory
- add plugin sysntax n config file
- you can add n number of plugins

```bash
[iventory]
enable_plugins = host_list, script, auto, yaml, ini
```
- Install `boto3` in python virtual invorment
```bash
pip3 install boto3
pip3 install botocore
```
- Add access key and Secret key using export
```bash
# create .yml file for AWS plugin
plugin:amazon.aws.aws_ec2

# verify and populate he AWS dynamic inventory
ansible-inventory -i <AWS plugin File name> --graph

```
___________________________________________________

## Ansible Playbooks 

### Indicator Characters
| | Symbol|Functionality|
|--------|--------|------|
| 1 | : | It is used to describe the mapping value.
| 2 | - | It describes the entry of the block sequence.
| 3 | , | It describes the entry of flow collection.
| 4	| ?	| It is used to describe the mapping key.
| 5	| !	| It describes the tag of a node.
| 6	| &	| It describes the anchor property of a node.
| 7	| |	| It is used to describe the literal block scalar.
| 8	| #	| It is used to describe the comments.
| 9	| >	| It is used to describe the folded block scalar.
| 10 | { | It is used to start the mapping of flow.
| 11 | } | It is used to end the mapping of flow.
| 12 | [ | It is used to start the sequence of flow.
| 13 | ] | It is used to end the sequence of flow.
| 14 | % | It describes the use of directives.
| 15 | * | It is used to describe the alias node.

### What is Ansible Playbook
- **Ansible Playbooks** are plain-text files written in YAML, which stands for *YAML Ain't Markup Lanugage.* and which have extension **.yaml or .yml**
- It consist of **Plays** which defines a set of tasks to be performed on hosts. 
- It is commonly used for configuration Management.
- It is a case sensitive scripting language.
- It sends the commands to remote server in scripted way instead of using Ansible commands indviually to configure remote server from command line.
- YAML uses “`|`” to include newlines while showing multiple lines and “`>`” to suppress newlines while showing multiple lines. 
- Due to this we can read and edit large lines. 
- In both the cases intendentation will be ignored.
 

> **Note** YAML files must start with a single dash (-) or triple dashes (---). 

**Task** Install a apache server on remote machine.

**Play** Consist of 1 or more tasks like install apache server and start the service

**Playbook** Composed or 1 or more play

<br>

### Different YAML tags in playbook

**name** 
- This tag specifies the name of the Ansible play.
- As in what this playbook will be doing. 
- Any logical name can be given to the playbook.

**hosts**
- This tag specifies the lists of hosts or host group against which we want to run the task. 
- The hosts field/tag is mandatory. 
- It tells Ansible on which hosts to run the listed tasks. 
- The tasks can be run on the same machine or on a remote machine. 

**become**
- yes or no not previladges

**become_user**
- name of user

**vars**
- Vars tag lets you define the variables which you can use in your playbook. 
- Usage is similar to variables in any programming language.

**tasks**
- Tasks are a list of actions one needs to perform. 
- A tasks field contains the name of the task. 
- Each task internally links to a piece of code called a *module*. 
- A `module` that should be executed, and arguments that are required for the module you want to execute.	  

### Ansible Playbook Structure

- Each playbook is an aggregation of one or more plays in it. 
- Playbooks are structured using Plays. 
- There can be more than one play inside a playbook.
- The function of a play is to map a set of instructions defined against a particular host.
- `YAML` is a strict typed language; so, extra care needs to be taken while writing the YAML files.

**Tips:**
1. You can check yaml file systax check before run using `--syntax-check`
2. You can run in dry-run state means no change will do on remote servers, use using `--check` at end of ansible-playbook command.
3. For verbose output using `-v`
4. Logging msg to print then use `dbug Module` have 3 parameters:

```bash
msg # - print or logging statement
var #- variable which value user want to print
verbosity #- Define verbosity of messages
```

```yaml
- name: This tells what the play is about
  host: This could be a single target host or the group-name of hosts
  tasks:
      - name: Description of task 1
      - name: Description of task 2
```

| Item  | Description |
| ------------- | ------------- |
| `ansible-playbook <YAML>` | Run on all hosts defined |
| `ansible-playbook <YAML> -f 10` | Run 10 hosts parallel |
| `ansible-playbook <YAML> --verbose` OR `-v` | Verbose on successful tasks |
| `ansible-playbook <YAML> -C` OR `--syntax-check`| Syntax check |
| `ansible-playbook <YAML> -C -D` OR `--chcek` | Dry run |
| `ansible-playbook <YAML> -l <host>` OR `--limit <hosts/group>` | Run on single host/group |


## MODULES ##
- The different actions run by tasks are called modules. 
- Modules are idempotent in ansible meaning if you run a playbook with the same set of inputs, you should not expect it to make any changes on the system0.

| Item  | Description |
| ------------- | ------------- |
| `copy`  | copy file or content |
| `get_url`  | download file |
| `file`  | manage file/directories |
| `yum`  | manage package |
| `service`  | manage services |
| `firewalld`  | firewall service |
| `lineinfile`  | add a line to dest file |
| `template`  | to template file with variables |
| `debug` | to debug and display |
| `add_host` | add host to inventory while play |
| `wait_for` | use for flow control  |
| `command` | use for execute commnad on remote host  |
| `script` | use for run script on remote host  |
| `wait_for` | use for flow control  |

<br>

### COMMAND MODULE
- Executes a command on a remote node.

```yaml
- name: Demo of using command module
  hosts: server1
  tasks:
    - name: 'Check date'
      command: date
      register: date
      
    - name: 'Display test-file.conf contents'
      command: cat /etc/test-file.conf
      register: display

    - name: 'Switch first to /etc then display test-file.conf contents'
      command: chdir=/etc cat test-file.conf 
      register: change

#  This will show the output of the tasks 1-3.
    - name: 'Show variables'
      debug:
        msg: "{{date}}"
    - name: 'Show variables'
      debug:
        msg: "{{display}}"
    - name: 'Show variables'
      debug:
        msg: "{{change}}"
```

### SCRIPT

- Runs a local script (located on the master or controller machine) on a remote node after transferring it. 
- The way ansible does this, it copies the script onto the remote nodes and runs them there.

A sample playbook which uses the script module:

```yaml
-
- name: Demo for usign script module
  hosts: all
  tasks:
    - name: Run script on remote server
      script: /some/local/script.sh -arg1 -arg2
```

### SERVICES MODULE

- Used to manage and maintain services on a system. 
- This includes **start, stop,** or **restarting** services.
- Actions/state `reloaded` `restarted` `started` `stopped`

```yaml
- name: Start services in order
  host: all
  tasks:
    - name: Start the DB service
       service: 
        name: mysql 
        state: started/stopped/restarted/reloaded
```
<br>

### LINEINFILE MODULE 

- Search for a line in a file and replace it or add it if it does not exist. 
- For example, we're given a task to add servers to the /ansible-test/sample-file.txt file in server1. 
- (Note that you shuold have a ~/ansible-test/sample-file.txt in server1)
- The way to do this is to use the lineinfile module.

```yaml
-  name: Add servers to /ansible-test/sample-file.txt on server1
   hosts: server1
   tasks:
       - name: Add first server to /ansible-test/sample-file.txt
           lineinfile: 
               path: ~/ansible-test/sample-file.txt
               line: 'server 10.0.0.125'
       - name: Add second server to /ansible-test/sample-file.txt
           lineinfile: 
               path: ~/ansible-test/sample-file.txt
               line: 'server 10.0.0.126'
```

```bash
ansible-playbook add.yaml -i inventory.txt 
```
<br>

```yaml
# Ping module with gather facts no
# on backend it uses by default setup module
---
- name: Ping connection
  hosts: all
  gather_facts: no
  remote_user: ansible
  tasks:
    - name: Test connection
      ping:
      remote_user: ansible
...
--------------------
# Ping module with gather facts yes
---
- name: Ping connection
  hosts: all
  gather_facts: yes
  remote_user: ansible
  tasks:
    - name: Test connection
      ping:
      remote_user: ansible

----------------------
# create file on remote host
---
- name: create file on remote host
  hosts: appServer
  tasks:
   - name: Create a file
     file:
      path: /tmp/new_file.txt 
      state: touch
...

-----------------------
# This playbbok will install HTTP server and start the server.
# Task1: Install Apache HTTP server
# Task2: Start HTTP Server
# Task3: Insert Index Page
# Task4: Task for Debug module to print or messaging
# Module used: yum, service, template, debug

---
- name: Install Apache Web server
  hosts: appServers
  become: true
  tasks:
    - name: Install Apache HTTP server
      yum: 
       name: httpd 
       update_cache: yes 
       state: latest

    - name: Start HTTP Server
      service: 
       name: httpd 
       enabled: yes 
       state: started

    - name: Insert Index Page
      template:
       src: index.html
       dest: /var/www/html/index.html

    - name: Task for Debug module
      debug:
       msg: "Apache installed succesfully" 

    - name: multilene msg
      debug:
       msg: 
        - "Apache installed succesfully"
        - "Second line msg" 

    - name: Print variable
      debug:
       msg: 
        - "Host IP is - {{ inventory_hostname }}"
        - Host IP is - {{ inventory_hostname }}

# var in debug module

    - name: Print  another way to variable
      debug:
       var: inventory_hostname 

# run playbook with number of -v to match the number in verbosity in playbook

    - name: Verbosity in debug module
      debug:
       msg: "This is deep logging at gbug level 2"
       verbosity: 2 

...
```

## Variables
- Vars defines the variables which you can use in your playbook. 
- Its usage is similar to the variables in any programming language.
- Variables can also be created on a separate file and this separate file can just be referenced by the playbook ( **host_vars** and **group_vars** )
- We can configure variables in the playbook itself using the **vars** keyword, followed by the key-pairs. 

- We can define inventory based variables in the below path that's applicable globally for all hosts:
  - group_vars/all
  - group_vars/groupname
  - host_vars/hostname

| Item  | Description |
| ------------- | ------------- |
| `host_vars`  | directory for host variable files  |
| `group_vars` | directory for group variable files |
| `facts` | collecting the host specific data |
| `register` | registered variables |
| `vars` | in playbook |
| `vars_files` | in playbook |
| `include_vars` | module |
| `include_tasks: stuff.yml` | include a sub task file |

### Fact variables
Fact variables are runtime variables that get generated when setup module gets executed such as
- ansible_os_family
- ansible_processor_cores
- ansible_kernel
- ansible_default_ipv4

#### Use debug module in Ansible is to prints simple statements to stdout

```yaml
- name: Printing ansible distribution
  hosts: all
  tasks: 
     - name: Print 
       debug:
          var: ansible_distribution

```        
### Data collection in Ansible
- data collection or data store is used to store multiple values
- you can have sequence data structure
- you can have a map data structure

### Set_fact and register
- Ansible module generally return a data structure
- User can store the output of module using ansible `register` module
- We can also based the conditions on the output of the previous task. 
- We can save the output or returned value of the preceeding task, and use that as basis of the condition. 
- To store the output of the previous task, we use the **register** followed by the variable we want to use.
- `Set_fact` is used to store the variable.

### Arithmaic Operations in Playbook
- Arithmetic operations in playbook is possible with jinja Syntax.
- `{{ variable_name }}` is a jinja yntax


### Filter and Methods in playbok
- Filter and Methods are the ways to performoperations on your variables.
- Filter: Inbuild operation definition in ansible (jinja2 template) use `|`
- Methods: Python methods, custom filters use `.`
- you can use |int, |upper, |lover, |title
- you can use .upper(), .lover(), .title()

<br>


## Operator Conditionl Statements

### Comparison Operator
- comparision operatiors are helpful to work with conditional operatior.
- Comparision operators are always return either True of False
- `==`, `!=` `>`, `>` `<=` `>=` 

### Membaeship operator

- Membaeship operator alsso return True of False
- `in` and `not in` are the membership operator
- Test operator are useful to perform the validationin ansible
- Tests for variables:
1. is define
2. is undefine

- Tests for string:
1. string is lower
2. string is upper
3. string is string

- Tests for numbers:
1. Number is divisible by number
2. Nummber is even
3. Number is odd
4. Number is number

- Tests for Paths:
1. Path is a directory
2. Path is a file
3. Path is link
4. Path is exists or not

### Logical Operator
- `and` and `or` are logical operators


| Condition1 | Condition2  | And | OR | 
|---------- | ---------- | --------- | --------- | 
| False     | False  | False| False|
| False     | True  | False | True|
| True      | False  | False| True|
| True     | True | True | True|

## Conditional statements and loops

| Item  | Description |
| ------------- | ------------- |
| `with_items` | then “item” inside action |
| `with_nested` | for nested loops |
| `with_file` | |
| `with_fileglob` | |  
| `with_sequence` | |
| `with_random_choice` | |
| `when` | meet a condition |

**when**
- Conditions in playbook are same as `if/else` conditions in programming, use **when** in Ansible.
- `failed_when`
- `changed_when`   

- In the example below, we have a playbook which checks the status of httpd. 
- If the service went down, it should send an email.

```yaml
- name: Check status of httpd service and send email if down.
  hosts: server1
  tasks:
    - name: Check status of httpd
      command: service httpd status
      register: status_var
    - name: Send email if down
        mail:
          to: admin@corp.com
          subject: Service Alert
          body: Hi, HTTPD service is down.
          when: status_var.stdout.find('down') != -1
```

- The first task is first executed. 
- It will run the *service httpd status* command on ht e linux machine and the output will be stored in the variable **status-var** which will be used in the second task.

```yaml
        -   
            name: Check status of httpd
            command: service httpd status
            register: status_var
```

- Now for the second task, we try to read this from the bottom again. 
- The condition here is to check the variable **status_var** and **find** for the word **"down"**. 
- If the word in not found in the variable, it wll return a value of **-1**.
- Otherwise, the value will not be **-1** and it will proceed with the task of 
sending the email.

```yaml
- name: Send email if down
  mail:
    to: admin@corp.co
    subject: Service Alert
    body: Hi, HTTPD service is down.
    when: status_var.stdout.find('down') != -1
```
<br>

- Here we have two playbooks that does the same thing but on different OS - install NGINX. 
- Both install packages differently Debian distros use *apt* while RedHat uses *yum*.
- Beside the package manager, you'll also have to specify different *hosts* for each one. Having two playbooks is alright but it can be done altogether using just one. 
- This is where **conditionals** comes into play.

Syntax: 
```yaml
      tasks:
         - name: Install httpd service Ubuntu
           yum: 
             name: httpd
             state: present
           when: ansible_distribution == 'Ubuntu'
         - name: Install httpd service Centos 
           apt:
             name: httpd
             state: present
           when: ansible_distribution == 'Centos'
```    

- We can do a single playbook with two tasks and then we specify the conditions under each task.

```yaml
-
    name: Install NGINX on Linux machines
    hosts: all
    tasks:
        -
            name: Install NGINX on Debian
            apt:
                name: nginx
                state: present
            when: ansible_os_family == "Debian" and
                  ansible_distribution_version == "18.04"
        -       
            name:
            yum:
                name: nginx
                state: present
            when: ansible_os_family == "RedHat" or
                  ansible_os_family == "SUSE"
```

- Notice that for the **conditional statements**, we use the keyword **when**. 
- We also use logical operators **and**, **or**, and the **'=='**. 
- In addition to this, we also specify that **apt** is to be used for the first task while **yum** on the second one.

- We use the **and** operator to tell Ansible to make sure both specified conditions are fulfilled. 
- In this case, nginx will only be installed if the OS is Debian *and* the version on that machine is 18.04.

```yaml
            when: ansible_os_family == "Debian" and
                  ansible_distribution_version == "18.04"
```
- On the other hand, we use **or** if atleast one of the conditions is required to be true, and not both.

```yaml
            when: ansible_os_family == "RedHat" or
                  ansible_os_family == "SUSE"
```   
### Install multiple packages

```yaml
    tasks:
         - name: Install httpd, git, zip service in Ubuntu
           yum: 
             name: "{{item}}"
             state: present
           when: ansible_distribution == 'Ubuntu'
           loop:
             - httpd
             - git
             - zip
         - name: Install httpd, git, zip service in Centos 
           apt:
             name: "{{item}}"
             state: present
             update_cache: yes
           when: ansible_distribution == 'Centos'
           loop:
             - httpd
             - git
             - zip
```     
- In the [create-user.yaml](create-user.yaml) below, we'll be using the **user module** to create users on the target machines. As you can see, this is not efficient since we have multiple tasks that just does the same thing.

```yaml
-
    name: Create users
    hosts: server1
    tasks:
        -
            user: name=john state=present
        -
            user: name=jane state=present
        -
            user: name=jeff state=present
        -
            user: name=sam state=present
        -
            user: name=ron state=present
        -
            user: name=mack state=present
```
- So we modified the [create-user.yaml](create-user.yaml) to include just one task and **loop over the list** of users.

```yaml
-
    name: Create users
    hosts: server1
    tasks:
        -
            user: name="{{ item }}" state=present
            loop:
                - john
                - jane
                - jeff
                - sam
                - ron
                - mack
```
- Now let's say we want to create a user and a corresponding user ID. This would mean we have to loop over a set of *key-pair* values. For this one, we can use **dictionaries**. We have created a second playbook below, [create-user-id.yaml](create-user-id.yaml) which does exactly that.

```yaml
-
    name: Create user with corresponding user ID
    hosts: server1
    tasks:
        - 
            user:
                name: "{{ item.name }}"
                uid: "{{ item.uid }}"
                state: present
            loop:
                - 
                    name: john
                    uid: 1000
                - 
                    name: jane
                    uid: 1001
                -
                    name: jeff
                    uid: 1002
                - 
                    name: sam
                    uid: 1003
                - 
                    name: ron
                    uid: 1004
                -
                    name: mack
                    uid: 1005
```
- In another example, we see another way to write loops using **with_items**.

```yaml
-
    name:
    hosts:
    tasks:
        -
            user: 
                name: "{{ item.name }}"
                uid: "{{ item.uid }}"
                state: present
            with_items:
                - john
                - jane
                - jeff
                - sam
                - ron
                - mack
```

- The **with_** can also be useful in other instances, like handling files, working on a set of URLs, or connecting to multiple database.

- Note that each one used their own keyword. There are a lot more of these, but below  are just some example.
- `with_files`
- `with_url`
- `with_mongodb`

## Loop with list
	
### This will run debug three times since the list is flattened
```yaml
- debug:
    msg: "{{ item }}"
  vars:
    nested_list:
      - - one
        - two
        - three
  with_items: "{{ nested_list }}"

# This will run debug once with the three items
- debug:
    msg: "{{ item }}"
  vars:
    nested_list:
      - - one
        - two
        - three
  with_items:
    - "{{ nested_list }}"	


# Nested Loop

- name: give users access to multiple databases
  mysql_user:
    name: "{{ item[0] }}"
    priv: "{{ item[1] }}.*:ALL"
    append_privs: yes
    password: "foo"
  with_nested:
    - [ 'alice', 'bob' ]
    - [ 'clientdb', 'employeedb', 'providerdb' ]

### In  below script there will be a nested loop for user1 value 1,2 means loo
---
 - hosts: 172.31.27.53
   vars:
     user1:
      - 1
      - 2

   tasks:
    - name: Creating multiple users
      debug:
        msg: "{{ item }}"
      with_nested:
       - "{{ user1 }}"
       - [ 3 , 4 ]

### You can loop through the elements of a hash using with_dict like below:
---
 - hosts: 172.31.27.53
   vars:
     users:
       raman:
        name: raman
        age: 40
        Add:
         city: Bangalore
       test:
        name: raj
        age: 35
        Add:
         city: Delhi

   tasks:
    - name: Creating multiple users
      debug:
        msg: "{{ item.value.Add.city }} {{ item.value.name }}"
      with_dict:
       - "{{ users }}"

	   
### reading the local files using with_file

---
 - hosts: 172.31.27.53
   tasks:
    - name: reading the content of the files
      debug:
        msg: "{{ item }}"
      with_file:
       - /tmp/1.txt
       - /tmp/2.txt

----------------------------------------------------------------------

### **CONDITIONALS IN LOOPS**
- We can also use conditions on loops. 
- For the example below, we will be installing different services on a Debian machine. 
- We can set the packages as a variable.

```yaml
- name: Install services
  hosts: all
  vars:
    packages:
            - name: nginx
              required: true
            - name: mysql
              required: true
            - name: apache
              required: false
  task:
    - name: Install "{{ item.name }}" on Debian
        apt:
          name: {{ item.name }}
          state: present
        when: item.required == true
        loop: "{{ packages }}"
```
- The way I understood this is by reading the YAML from bottom to top. 
- The first point we have here is we are **looping or iterating over the packages**.

```yaml
            loop: "{{ packages }}"
```
- The packages referred in this instance is a variable which contain a set of packages along with an attribute *required* 
- basically the packages is a **list**. So we are simply **iterating over the list** and each package on that list is an **item**

```yaml
    vars:
        packages:
            -
                name: nginx
                required: true
            -
                name: mysql
                required: true
            -
                name: apache
                required: false
```
- Now it goes over the first item, which is an nginx. It check if the attribute **required** is set to true, in which case, it will proceed with the task and install nginx using yum.
- Otherwise, it won't do anything. 
- It repeats the process onto the second item, the third item, until it reaches the end of the list.

```yaml
    task:
        -
            name: Install "{{ item.name }}" on Debian
            apt:
                name: {{ item.name }}
                state: present
            when: item.required == true
```

<br>


-----------------------------------------------------------

### Loops in Ansible
- Loops are used to iterate the condition in playbook for diffrent servers.
- Loops are helpful idf user wants to perform many things in one task, such as ctreate lots of users, install multiple packages, etc....
- Standerd Loops with `with_items`


**Syntax**

```yaml
---
- name: add several users all in once
  user:
    name: "{{ item.name }}"
    state: present
    groups: "user"
  with_items:
    - testuser1
    - testuser2
...
```
- Multiple items in one itrate

```yaml
---
- name: add several users
  user:
    name: "{{ item.name }}"
    state: present
    groups: "{{ item.groups }}"
  with_items:
    - { name: 'testuser1', groups: 'wheel' }
    - { name: 'testuser2', groups: 'root' }
...
```
<br>


- `Random Choise Loops`
- Its can pickup any task randomlly

```yaml
---
- name: add several users all in once
  debug:
    msg: "{{ item }}"
  with_random_choise:
    - "Left"
    - "Right"
    - "UP"
    - "Down"
...
```
- `Do-Until Loop` - To retry a task until a certain condition is met.
- Default value for `retries` is 3, and `delay` is 5 sec
- We can chage as per our requirnment

```yaml
    - name: apache is running
      service:
        name: httpd
        state: restarted
      register: result
      until: result.changed == True
      retries: 7
      delay: 5
```

- Install Multiple Packages using `loop` or can use `with_item`

```yaml
#!/root/ansible/myansible/bin/ansible-playbook
- name: Loops in Ansible Playbook Part III
  hosts: all
  remote_user: ec2-user
  become: 'yes'
  become_user: root

  vars:
    packages: [ 'gettext-devel', 'openssl-devel', 'perl-CPAN', 'perl-devel', 'zlib-devel', 'unzip', 'curl', 'wget' ]
  tasks:
    - name: Install Multiple Packages using Loop
      yum:
        name: '{{ item }}'
        state: present
      loop:
        - gettext-devel
        - openssl-devel
        - perl-CPAN
        - perl-devel
        - zlib-devel
        - unzip
        - curl
        - wget


    - name: UnInstall Multiple Packages using Index Loop
      yum:
        name: '{{ item.1 }}'
        state: absent
      with_indexed_items:
        - "{{ packages }}"


    - name: Install Multiple Packages using Index Loop
      yum:
        name: '{{ item.0 }}'
        state: present
      with_together:
        - "{{ packages }}"
```
<br>

## Handler in Ansible
- Sometimes you want a task to run only when a change is made on a machine. 
- For example, you may want to restart a service if a task updates the configuration of that service, but not if the configuration is unchanged. 
- Ansible uses `handlers` to address this use case. Handlers are tasks that only run when `notified`.

```yaml
  - name: Start NGiNX
    service:
      name: nginx
      state: started
      enabled: yes  # if you want to also enable nginx
    notify:
    - restart and enable httpd

  handlers:
    - name: restart and enable httpd
      become: true
      service:
        name: nginx
        state: restarted
        enabled: yes
```
<br>

## Tags in Ansible

- Tags can be added to a single task or include. You can also apply tags to numerous jobs by defining them at the block, play, role, or import level. All of these use scenarios are addressed by the keyword tags. 
- From below Plabook you can run playbook using tags
- Tags are case sensetice (Capital and small letters).

| Item  | Description |
| ------------- | ------------- |
| `tags` | add tags to the tasks |
| `--tags ‘<tag>’` | during playbook execution |
| `--skip-tags` | for skipping those tags |
| `tagged` | run any tagged tasks |
| `untagged` |any untagged items |
| `--list-tags` | list all tags in playbook |

```bash
ansible-playbook tags.yml --tags start

# Multiple tasks
ansible-playbook tags.yml --tags install, start

# skip
ansible-playbook tags.yml --skip-tags start

# List the number of tags in playbook
ansible-playbook tags.yml --list-tags

```
```yaml
---
- hosts: localhost
  become: yes
  tasks:

     - name: Install Apache HTTP server on RedHat Server
         tags:
           - install
         yum: 
           name: httpd
           state: present
         when: ansible_os_family == "RedHat"
      
      - name: Install Apache HTTP server on Ubuntu server
         tags:
           - install
           - start
         apt:
           name: apache2
           state: present
         when: ansible_os_family == "Debian"
      
      - name: Install Apache HTTP server on CentOS server
         yum: 
           name: httpd
           state: present
         when: 
           - ansible_facts['distribution'] == "CentOS"
           - ansible_facts['distribution_major_version'] == "7"
     
     - name: Print the Ansible free memory
         debug:
           msg: "free memory is {{ansible_memory_mb.real.free}}"
```
<br>

-----------------------------------------------------------

## Working with include and import module
- Inport task is static and include in dynamic
- With include task we can use variables in file names (Eg: OS family)

**Include Module**
- `Include Module` using Include module, user can add only tasks from other file to another playbook
- While including Task from one file to anotherPlaybook, use can perform variable substitution.

- Using `include module`, you can also include complete Playbook into another playbook.
- This can be useful to tie together a few independant playbooks into a larger.

**include_tasks module**

- `include_tasks module` - Include_task also working similar to include module. But there are few fundamental differences
- Only include tasks not used to include the complete playbook.
- At runtime, include_tasks will work as seperate task and user get the entry in output.

**import_task and import_playbook**
- its similar to inclue
- All import statements are pre-processed at the time playbooks are parsed.
- can no imort run time value

```yaml
# File 1 for task
- name: Play 1 - Task 2
  debug:
    msg: Play 1 - Task 2

## include_task
#!/root/ansible/myansible/bin/ansible-playbook
- name: This will show the use of include task
  hosts: localhost
  gather_facts: false

  tasks:
    - name: Play 1 - Task 1
      debug:
        msg: "Play 1 - Task 1"
    - include: tasks-1.yml

# Playbook run one by one
------------------------------------------------------
## file2 complete playbook
#!/root/ansible/myansible/bin/ansible-playbook
- name: Play 2 from Include
  hosts: localhost
  gather_facts: false

  tasks:
    - name: Play 2 - Task 1
      debug:
        msg: "Play 2 - Task 1"

# include_playbook.yml
#!/root/ansible/myansible/bin/ansible-playbook
- name: Including Include Playbook
  hosts: localhost
  gather_facts: false

  tasks:
    - name: Play 1 - Task 1
      debug:
        msg: "Play 1 - Task 1"

- include: play2.yml 
------------------------------------------------------------
# Include-atask module
# Here it shows that including task from othere file

#!/root/ansible/myansible/bin/ansible-playbook
- name: This will show the use of include task
  hosts: localhost
  gather_facts: false

  tasks:
    - name: Play 1 - Task 1
      debug:
        msg: "Play 1 - Task 1"
    - include_tasks: tasks-1.yml

-------------------------------------------------------------------------
# import_playbook
# same outout like include

#!/root/ansible/myansible/bin/ansible-playbook
- name: Including Import Playbook
  hosts: localhost
  gather_facts: false

  tasks:
    - name: Play 1 - Task 1
      debug:
        msg: "Play 1 - Task 1"

- import_playbook: play2.yml

```

## Ansible local_action module
- Ansible playbook and tasks are always tend to work on Ansible remote machine or client
- Sometimes user need to work on Ansible controller node to generate some dada, to do some modification in between of Playbook.
- Ansible `local_action` is used to process the module, task on local machine i.e Ansible controller machine.
- Its limited to ansible controler

## Ansible delegate_to module

| Item  | Description |
| ------------- | ------------- |
| `delegate_to: localhost` | run the task on localhost instead of inventory item |
| `delegate_facts` | assign the gathered facts from the tasks to the delegated host instead of current host |

- Ansible `delegate_to` module is used, when user wants to execute specific tasks to specific module.
- Ansible `delegate_to` is a directive, not an individual module, It integrates with othere module and it controls the task execution by deciding which host should run the task at runtime.
- you can define a hosts in delegate_to directive.
- Its not limited to ansible controler

```yaml
---
- name: Ansible Delegate_to examples
  hosts: all
  remote_user: ansible
  become: 'yes'
  become_user: root 

  vars:
    tmplog: /tmp/connection.log
  
  tasks:
  - name: create tmplog
    shell: test ! -f {{ tmplog }} && touch {{ tmplog }}
    failed_when: false
  
  - name: delegate_to
    shell: echo "delegate_to . {{ inventory_hostname }} $(hostname)" >> {{ tmplog }}
    delegate_to: ec2-13-59-156-142.us-east-2.compute.amazonaws.com
    run_once: true # to run only want execute task on above server

```

----------------------------------------------------
## Error Handling in Ansible

- In Ansible, when a particular command or module returns a zero code, the command is successfully executed without any failure. 
- If there is a non-zero code, which means this is a command failure, it will stop the execution on that particular host and continue on the other host.
- if there is no dependency I want to ignore


| Item  | Description |
| ------------- | ------------- |
| `ignore_errors` | proceed or not if any error on current task |
| `force_handlers` | call handler even the play failed |
| `failed_when` | mark the task as failed if a condition met |
| `changed_when` | set  “ok” or “failed” for a task |
| `block` | logical grouping of tasks (can use with when) |
| `rescue` | to run if block clause fails |
| `always` | always run even block success or fails |

```yaml
---
  - hosts: localhost
    gather_facts: fasle
    tasks:
      - command: "ls /home"
        register: home_out
        ignore_errors: yes
      - debug: var=home_out
      - command: "ls /tmp"
        register: tmp_out
      - debug: var=tmp_out
---------------------------------
---
  - hosts: localhost
    gather_facts: fasle
    become: yes
    tasks:
      - name: starting nginx
        service:
          name: nginx
          state: started
        ignore_errors: yes
      - name: starting httpd
        service:
          name: httpd
          state: started
---------------------------------
---
  - hosts: localhost
    gather_facts: false
    tasks:
    #  - command: "ls /home"
    #    register: out
    #    failed_when: out.rc==0 # return code
    #  - debug: var=out
      - command: "ls /home"
        register: out
      - fail:
          msg: "Failed because rc is 0"
        when: out.rc==0

# block is useful to group multiple tasks and we can apply some opetions like become, ignore_erros and when in block level instead of task level
---
  - hosts: web_servers
    gather_facts: true
    tasks:
      - block:
        - name: Installing htttpd for RedHat os family
          yum:
            name: httpd
            state: present
        - name: starting httpd for RedHat os family
          service:
            name: httpd
            state: started
        when: ansible_os_family=="RedHat"
        become: yes
      - block:
        - name: Installing apache2 for Debian os family
          apt:
            name: apache2
            state: present
        - name: starting apache2 for Debian os family
          service:
            name: apache2
            state: started
        when: ansible_os_family=="Debian"
        become: yes
      - debug:
          msg: "Succesfully completed all tasks"

---
# Error handling
# If it is success, ruscue is not execute 
# but always run whtaever will be the output of task
  - hosts: localhost
    gather_facts: false
    tasks:
      - block:
        - name: Finding files in /home/ansadmin/tomcat8
          command: "ls /home/ansadmin/tomcat8"
          register: tomcat8_out
        rescue:
          - debug:
             msg: "The given path: /home/ansadmin/tomcat8 is not a validpath"
        always:
          - debug:
             msg: "THis will always executes"

```

<br>


## Parallelism
| Item  | Description |
| ------------- | ------------- |
| 'forks' | number of forks or parallel machines|
| `--forks` | when using ansible-playbook |
| `serial` | control number parallel machines |
| `async: 3600` | wait 3600 seconds to complete the task |
| `poll: 10` | check every 10 seconds if task completed |
| `wait_for` |module to wait and check  if specific condition met |
| `async_status` | module to check an async task status |

<br>

## Jinja2 template 

- A Jinja2 template file is a text file that contains variables that get evaluated and replaced by actual values upon runtime or code execution. 
- In a Jinja2 template file, you will find the following tags:

**{{ }}**  : These double curly braces are the widely used tags in a template file and they are used for embedding variables and ultimately printing their value during code execution. For example, a simple syntax using the double curly braces is as shown: The {{ webserver }} is running on  {{ nginx-version }}
**{%  %}** : These are mostly used for control statements such as loops and if-else statements.
**{#  #}** : These denote comments that describe a task.

```yaml
- name: Copy a version of named.conf that is dependent on the OS. setype obtained by doing ls -Z /etc/named.conf on original file
  ansible.builtin.template:
    src: named.conf_{{ ansible_os_family }}.j2
    dest: /etc/named.conf
    group: named
    setype: named_conf_t
    mode: 0640
```
```yaml
---
- hosts: worker1
  become: yes
  vars:
    usernames: ['Alice', 'Bob', 'John', 'Martin', 'Alex']

  tasks:
    - name: Loops usage within Jinja2 templates
      template:
        src: usernames.j2
        dest: /home/ansible_user/usernames.txt
```
cat usernames.j2
```yaml
<html>
    <center>
        <h1> Welcome to {{ company_name }}. This webserver is hosted on {{ ansible_hostname }}. </h1>
    </center>
</html>

# The list of users who are going to be part of the ongoing migration process.

{% for item in usernames %}

   {{ item }}

{% endfor %}
```

-----------------------------------------------------------

## Ansible Roles

-  To reuse play book there are 2 ways
  - roles
  - include
 
- In Ansible, the role is the primary mechanism for breaking a playbook into multiple files.
- Roles allows you to reuse the common configuration step between different types of steps.
- Roles are flexible and easily modified.
- This simplifies writing complex playbooks, and it makes them easier to reuse.
- Roles in Ansible are next level of abstraction of Ansible playbooks

#### Benefits of Ansible Roles
- idea of include files and combine them to form clean and resuable abstraction
- Easy to maintain/troubleshooting the playbooks
  
#### Structure of Roles

| Item  | Description |
| ------------- | ------------- |
| `defaults` | Stores data about roles and default variables. |
| `files` | Store files which is to be pushed to the remote machine. |
| `handlers` | Tasks that get triggered from some action. |
| `meta` | role info like Author, Licence, Platform, etc |
| `tasks` | Contains main list of tasks to be executed by roles. |
| `templates` | jinja2 templates. Contains Templates which can be deployed via role. |
| `tests` | test inventory and test.yml |
| `vars` | Stores variables with high priorty than default variables. |
| `pre_tasks` | tasks before role |
| `post_tasks` | tasks after role |
| `pre_tasks` | tasks before role |
| `post_tasks` | tasks after role |

#### Command to create role offline/ your own role
```bash
ansible-galaxy init apache --offline
```

main.yml
```yaml
---
# tasks file for apache
- include: install.yml
- include: configure.yml
```

install.yml
```yaml
---
 - name: installing httpd
   apt:
    name: apache2
    state: present
```

configure.yml
```yaml
---
- name: status
  copy: src=status.txt dest=/tmp/status.txt
  notify:
     restart apache service
- name: send the file
  copy: src=test.html dest=/var/www/html/test.html
```
- copy the configuration file to files/ folder

```bash
cp /etc/httpd/conf/httpd.conf .
```
- under handlers folder/main.yml

```yaml
---
# handlers file for apache
- name: restart apache service
  service: name=apache2 state=restarted

# Call the proceudre in the main yaml file  
  ---
 - hosts: webservers
   roles:
        - apache
```

#### Command to create role using ansible galaxy
- To create ansible role, use `ansible-galaxy init <role_name>` to create the role directory structure.
```bash
ansible-galaxy init <role_name>
ansible-galaxy search apache
galaxy.ansible.combine
```
- https://galaxy.ansible.com

| Item  | Description |
| ------------- | ------------- |
| `ansible-galaxy search ‘install git’ --platform el` | search for a role |
| `ansible-galaxy info <role-name>` | display role information |
| `ansible-galaxy install <role-name> -p <directory>` | install role from galaxy |
| `ansible-galaxy list` | to list local roles |
| `ansible-galaxy remove <role-name>` | remove role |
| `ansible-galaxy init --offline <role-name>` | initiate a role directory |

-----------------------------------------------------------

## Ansible Vault

| Item  | Description |
| ------------- | ------------- |
| `ansible-vault create newfile` | create a new vault file |
| `ansible-vault view newfile` | view file which is already ansible vaulted |
| `ansible-vault edit newfile` | Edit file |
| `ansible-vault view --vault-password-file .secret newfile` | Provide vault password as file |
| `ansible-vault decrypt newfile` | Remove encryption or vault |
| `ansible-vault rekey newfile` | change vault password |
| `--ask-vault-pass` or <br /> `--vault-password-file <secret-password-file>` | ask for vault password for ansible-playbook

- Ansible Vault is a feature of ansible that allows you to keep sensitive data such as passwords or keys in encrypted files, rather than as plaintext in playbooks or roles. 
- These vault files can then be distributed or placed in source control.
- Ansible automatically decrypts vault-encrypted content at runtime when the key is provided.

**To check all the option available in ansible-vault**
```bash
ansible-vault -h
```

**Creating New Encrypted Files**
```bash
ansible-vault create vault.yml
cat vault.yml
```

**Encrypting Existing Files**
```bash
ansible-vault encrypt encrypt.yml
cat encrypt.yml
```

**Viewing Encrypted Files**
```bash
ansible-vault view vault.yml
```

**Editing Encrypted Files**
```bash
ansible-vault edit vault.yml
```

**Manually Decrypting Encrypted Files**
```bash
ansible-vault decrypt vault.yml
```

**Changing the Password of Encrypted Files**
```bash
ansible-vault rekey encrypt.yml
```

**Run encrypted playbook**
```bash
#Try without vault password
ansible-playbook web.yaml
ansible-playbook web.yaml  --ask-vault-pass
ansible-playbook web.yaml  --vault-id pass-file

```
## AWX
https://adamtheautomator.com/ansible-awx/

## jenkis with Ansible
https://medium.com/appgambit/ansible-playbook-with-jenkins-pipeline-2846d4442a31

## Troubleshooting
| Item  | Description |
| ------------- | ------------- |
| log_path | where logs are saved |
| `debug` | module for debugging |
| `--syntax-check` | syntax checking for playbooks before they run |
| `--step` | run playbook step by step |
| `--start-at-task`| run a playbook but start at specific task |
| `--check` | check mode |
| `--diff` | will show the expected changes if you run the playbook, but will not do any changes (kind of dry run) |
| `uri` | module for testing url |
| `script` | module for running script and return success code |
| `stat` | module to check the status of files/dir | 
| `assert` | check file exist |

## Running Ansible through SSH Jump / Bastion Host

- In a strict secured environment, you may not be allowed to connect to the ansible controlled server directly. 
- Only the bastion host (a.k.a jump host) is the one freely allowed to access all systems. 
- How will you perform your automation tasks in such scenario?

- As you can see from the diagram, we need to setup 2 different SSH keys first.
  - SSH key for connecting from Ansible server to the jump / bastion host. This can be user / root key.
  - SSH key from jump / bastion host to all target servers. This can also be either user or root key.

#### Configure the /etc/ansible/ansible.cfg file and enter the path of private key file.
```bash
grep private_key_file /etc/ansible/ansible.cfg
private_key_file = ~/.ssh/bastion
```

#### Update Host Variables in the inventory
```bash
[server]
controlledserver

[server:vars]
ansible_ssh_common_args='-o StrictHostKeyChecking=no -o ProxyCommand="ssh -W %h:%p -q <user>@bastion"'
ansible_ssh_user=<user>
```
- In this inventory section, you have to define 2 variables. 
- First one is `ansible_ssh_common_args` and second one is `ansible_ssh_user`. 
- The common argument parameter will define `SSH proxy` for all hosts defined under that host group. 
- If you want strict host key checking to be enabled, you can remove the line `-o StrictHostKeyChecking=no`.

- Now, I have defined a parameter `ansible_ssh_user`. 
- This will tell Ansible that when you connect from jump host to target servers, use that user. 
- If you don’t define any user here, Ansible will assume that you are running the command as root user. 
- If you want to run as root user, then your SSH Key 2 should be root user key of the jump host.
- `j` ProxyJump 


## Patching using Ansible
- Examlple 1
```yaml
- name: Patching Linux server
  hosts: all
  become: yes
  tasks:
  - name: patch
    yum:
     name: '*'
     state: latest
     exclude: docker-ce*
     update_only: true # update only installed packages
     download_only: true # only download not install

```
- Examlple 2 https://www.youtube.com/watch?v=7al0yehXa_g&ab_channel=YogeshMehta
```yaml
- name: Patching 
  hosts: dev-redhat
  serial: 2
  tasks:
    # purpose of this task to check if app is running or not
    - name: Verify app/DB is running
      shell: if ps -eaf | grep 'apache|httpd' | grep -v grep > /dev/null; then echo 'process_running'; else 'process_not_running'; fi
      ignore_errors: true
      register: app_process_check

    # This is decision play, Play will check will fail/quit, if app running
    - name: decision point to start patching
      fail: msg="{{ inventory_hostname}} have not running application first, then attempt patching
      when: app_proces_check == 'process_running'

    # this task will upgrade/install the rpm's if app is stopped
    - name: upgrade all packages on the server
      yum:
       name: "kernel" # * means all
       state: latest
      when: app_process_check.stdout == "process_not_running" and ansible_distribution == 'CentOS' or ansible_distribution == 'Red Hat Enterprise Linux'
      register: yum_update

    #  If Kernel installed rebbot need oothrewise not needed

    # reboot

    # task to wait for 3 min
    - name: pause for 180 sec
      pause:
        minutes: 3

    # Check with local action whether reboot completed or not





```

## Ansible and jenkins

- https://www.youtube.com/watch?v=Pd1L4sj-vyg&ab_channel=PowerCloud

### Example 1

- https://medium.com/@selvamraju007/ansible-playbook-with-jenkins-pipeline-1bd981d4fe2f

#### Ansible Playbook With Jenkins Pipeline

- create Ansible Playbook for copying .jar file from GitHub to remote server 
- write Jenkins pipeline script to execute the job.

```yaml
---
- name: Copy jar file from GitHub to server
  hosts: your_server
  gather_facts: false

  vars:
    github_repo_url: "https://github.com/your_github_username/your_github_repo.git"
    jar_file_path: "your_jar_file.jar"

  tasks:
    - name: Clone GitHub repository
      git:
        repo: "{{ github_repo_url }}"
        dest: "/tmp/your_github_repo"
        version: master

    - name: Copy jar file to server
      copy:
        src: "/tmp/your_github_repo/{{ jar_file_path }}"
        dest: "/home/your_username/{{ jar_file_path }}"

```

```
pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    credentialsId: 'your_github_credentials',
                    url: 'https://github.com/your_username/your_repository.git'
            }
        }
        stage('Execute Ansible playbook') {
            steps {
                ansiblePlaybook playbook: 'copy_jar_file.yml'
            }
        }
        stage('Transfer jar file') {
            steps {
                script {
                    def servers = ['server1.example.com', 'server2.example.com', 'server3.example.com']
                    servers.each { server ->
                        sshPublisher(
                            sshPublisherDesc: [
                                configName: 'your_ssh_credentials',
                                hostname: server
                            ],
                            transfers: [
                                sshTransfer(
                                    cleanRemote: false,
                                    excludes: '',
                                    execCommand: '',
                                    flatten: false,
                                    makeEmptyDirs: false,
                                    noDefaultExcludes: false,
                                    patternSeparator: '[, ]+',
                                    remoteDirectory: '/home/your_username/',
                                    remoteDirectorySDF: false,
                                    remoteFiles: 'your_jar_file.jar',
                                    removePrefix: '',
                                    sourceFiles: 'your_jar_file.jar'
                                )
                            ]
                        )
                    }
                }
            }
        }
        stage('Deploy jar file') {
            steps {
                script {
                    def servers = ['server1.example.com', 'server2.example.com', 'server3.example.com']
                    servers.each { server ->
                        sshPublisher(
                            sshPublisherDesc: [
                                configName: 'your_ssh_credentials',
                                hostname: server
                            ],
                            publishers: [
                                sshPublisherDesc(
                                    transfers: [
                                        sshTransfer(
                                            cleanRemote: false,
                                            excludes: '',
                                            execCommand: 'sudo systemctl stop your_service_name',
                                            flatten: false,
                                            makeEmptyDirs: false,
                                            noDefaultExcludes: false,
                                            patternSeparator: '[, ]+',
                                            remoteDirectory: '/home/your_username/',
                                            remoteDirectorySDF: false,
                                            remoteFiles: '',
                                            removePrefix: '',
                                            sourceFiles: ''
                                        ),
                                        sshTransfer(
                                            cleanRemote: false,
                                            excludes: '',
                                            execCommand: 'sudo cp /home/your_username/your_jar_file.jar /opt/your_service_directory/',
                                            flatten: false,
                                            makeEmptyDirs: false,
                                            noDefaultExcludes: false,
                                            patternSeparator: '[, ]+',
                                            remoteDirectory: '/home/your_username/',
                                            remoteDirectorySDF: false,
                                            remoteFiles: '',
                                            removePrefix: '',
                                            sourceFiles: ''
                                        ),
                                        sshTransfer(
                                            cleanRemote: false,
                                            excludes: '',
                                            execCommand: 'sudo systemctl start your_service_name',
                                            flatten: false,
                                            makeEmptyDirs: false,
                                            noDefaultExcludes: false,
                                            patternSeparator: '[, ]+',
                                            remoteDirectory: '/home/your_username/',
                                            remoteDirectorySDF: false,
                                            remoteFiles: '',
                                            removePrefix: '',
                                            sourceFiles: ''
                                        )
                                    ]
                                )
                            ]
                        )
                    }
                }
            }
        }
    }
}

```

## raw module

- When python is not installed on remore server and we need to run commands we use `raw` module
- We use regular commands in " ".

```bash
ansible hosts -m raw -a "uptime"

```

