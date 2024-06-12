```yaml
--- 
- name: Install nginx
  hosts: all
  become: true

  tasks:
  - name: Add epel-release repo
    yum:
      name: epel-release
      state: present

  - name: Install nginx
    yum:
      name: nginx
      state: present

  - name: Insert Index Page
    template:
      src: index.html
      dest: /usr/share/nginx/html/index.html

  - name: Start NGiNX
    service:
      name: nginx
      state: started
      enabled: yes  # if you want to also enable nginx
      register: result
      until: result.rc == 0
      retries: 3
      delay: 5

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
### Retry block

```yaml
- command: /usr/bin/false
  retries: 3
  delay: 3
  register: result
  until: result.rc == 0
  
  retries: 3
  delay: 10
  until: outcome.result == 'success'
```

### Blockinfile

```yaml
- name: Add mappings to /etc/hosts
  ansible.builtin.blockinfile:
    path: /etc/hosts
    block: |
      {{ item.ip }} {{ item.name }}
    marker: "# {mark} ANSIBLE MANAGED BLOCK {{ item.name }}"
  loop:
    - { name: host1, ip: 10.10.1.10 }
    - { name: host2, ip: 10.10.1.11 }
    - { name: host3, ip: 10.10.1.12 }
```

```yaml
- name: Insert/Update eth0 configuration stanza in /etc/network/interfaces
        (it might be better to copy files into /etc/network/interfaces.d/)
  blockinfile:
    path: /etc/network/interfaces
    block: |
      iface eth0 inet static
          address 192.0.2.23
          netmask 255.255.255.0

```

### Envoirnment Variable


### Jinja2
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