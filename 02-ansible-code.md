```yaml
---
  - hosts: localhost
    gather_facts: fasle
    tasks:
      - command: "ls /homee"
        register: home_out
        ignore_errors: yes
      - debug: var=home_out
      - command: "ls /tmp"
        register: tmp_out
      - debug: 
          var: tmp_out
---------------------------------
```
```yaml
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
    #    failed_when: out.rc==0
    #  - debug: var=out
      - command: "ls /home"
        register: out
      - fail:
          msg: "Failed because rc is 0"
        when: out.rc==0
```
#block is useful to group multiple tasks and we can apply some opetions like become,ignore_erros and when in block level instead of task level
```yaml
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
          yum:
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
```

- This playbbok will install HTTP server and start the server.
```yaml
---
- name: Verify apache installation
  hosts: webservers

  vars:
    http_port: 80
    max_clients: 200
  remote_user: root
  
  tasks:
    - name: Add first server to /ansible-test/sample-file.txt
        lineinfile: 
            path: ~/ansible-test/sample-file.txt
            line: 'server 10.0.0.125'

    - name: Execute command to display the date.
      command: date

    - name: Execute script on server
      script: test_script.sh
 # tags
    - name: Ensure apache is at the latest version
      tags:
        - install
      yum:
        name: httpd
        state: latest
    - name: Ensure apache is running
      service:
        name: httpd
        state: restarted

    - name: Insert Index Page
# same can use copy module
      template:
       src: index.html
       dest: /var/www/html/index.html

    - name: Write the apache config file
      template:
        src: /srv/httpd.j2
        dest: /etc/httpd.conf
      notify:
      - Restart apache

  handlers:
    - name: Restart apache
      service:
        name: httpd
        state: restarted
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

---
- name:
  hosts:
  tasks:
    - user: 
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
...
```