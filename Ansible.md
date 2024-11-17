

### What is Configuration Management?
It means keeping all systems in your environment (like development, testing, and production) the same.
Ensures no configuration drift (when environments differ).
Helps avoid errors, simplifies debugging, and makes troubleshooting easier.

For example: If you’re installing a new version of a WebLogic or WebSphere server across 100 machines, doing it manually is a hassle. Instead, you can use Ansible to automate the installation on all machines simultaneously.

### What is Ansible?
 Ansible is an IT automation tool used for tasks like application deployment, server configuration, and orchestration.
Agentless: No need to install extra software (agents) on your machines. Ansible uses SSH (Linux) or WinRM (Windows) to connect.
Infrastructure as Code (IAC): You write instructions as code to manage systems, ensuring repeatability.
Developed in Python and acquired by Red Hat in 2015.

#### Key Features of Ansible
- Free and Open-Source: No license cost, free to use.
- **Agentless**: Connects directly to your systems without needing extra installations.
- Uses YAML Files:
- YAML = Yet Another Markup Language.
	- Human-readable format used for playbooks (scripts in Ansible).
	- Idempotent:
 - Ensures no repeated actions.
- **Example**: If a service is already running, Ansible won’t restart it unnecessarily.
- **Self-Documenting**: Playbooks describe the desired state clearly.
- **Error Recovery**: You can roll back to a previous configuration if something goes wrong.
- Ready-to-Use Modules:
- Pre-built modules for tasks like installing software, managing files, configuring networks, etc.
- Custom modules can be added if needed.

### How Ansible Works
**Control Machine**:
- The computer you use to run Ansible commands.
- Write an inventory file listing the IP addresses of all systems (nodes) you want to manage.
- Write a playbook describing the tasks (e.g., install software, restart services).
**Execution**:
- Ansible connects to the nodes via SSH/WinRM.
- Pushes small programs (called modules) to the nodes.
- Executes these modules and removes them after the task is complete.

### Why Use Ansible?
**Simplifies Automation**:
- Write once and run everywhere.
- Eliminates repetitive manual tasks.
- Multi-Tier Deployment:
- Designed for complex environments where multiple systems interact (e.g., deploying a web app with separate database and front-end servers).
- Cross-Platform:
	- Works on Linux, Windows, cloud, containers, etc.

### Ansible Tower
A GUI (Graphical User Interface) provided by Red Hat for managing Ansible.
Helps organize and monitor playbooks and tasks visually.

### What are Playbooks?
- Playbooks are simple text files written in YAML.
- They describe what state your system should be in.
- **Example**: Ensure a package is installed, a service is running, or a file is present.

### Idempotency in Ansible
Idempotent = No repeated changes if the desired state is already achieved.
Example:
- If a playbook says “Install Nginx,” Ansible first checks if Nginx is already installed.
- If yes, it does nothing. If not, it installs Nginx.

### Common Use Cases
**Configuration Management**: Set up servers with the exact configuration you want.
**Application Deployment**: Install apps on multiple machines with one playbook.
**Continuous Testing**: Keep applications updated and tested.
**Zero-Downtime Updates**: Deploy updates without downtime using rolling updates.
**Provisioning**: Set up servers in the cloud or on-premises.
**Orchestration**: Coordinate tasks across multiple systems (e.g., backend + frontend setup).

### Advantages of Ansible
**Easy to Learn**: Simple syntax and human-readable YAML files.
**Flexible**: Can be customized for unique tasks.
**Prevents Configuration Drift**: Keeps systems consistent.
**No Dependencies**: Doesn’t require databases, servers, or agents.

### Key Terminologies
**Inventory**: A list of systems (with their IPs) to manage.
**Playbook**: YAML file describing the desired state of systems.
**Module**: Pre-built scripts for common tasks (e.g., installing packages).

### State Checking in Ansible
Ansible checks the current system state before applying any changes.
**Example**: If a service is already running, Ansible doesn’t restart it.

# YAML Basics Explained

**YAML** (Yet Another Markup Language or YAML Ain't Markup Language) is a human-readable data serialization standard often used for configuration files. Here’s a breakdown of the key points:
Why YAML?

**Readability**: YAML is designed to be easy for humans to understand, with simple syntax compared to JSON or XML.
**Case Sensitivity**: YAML is case-sensitive; Key and key are treated as different.
**Indentation**: Indentation determines the structure and relationships in YAML. Use spaces, not tabs. Typically, 2 spaces are standard.
**File Extension**: YAML files use .yaml or .yml.

YAML Syntax and Structure

## Starting and Ending Syntax:
YAML files optionally start with --- and end with .... These markers are optional but help indicate the start and end of a YAML document.

## Comments:
Begin with #.

Example:
```yaml
# This is a comment
name: "John"
```

## Indentation:

Hierarchies are indicated by indentation (2 spaces). Tabs are not allowed.

Example:
```yaml
person:
  name: "Jane"
  age: 25
```

## Lists (Sequences):

Use a hyphen - followed by a space for each item in the list.

Example:
```yaml
languages:
  - Python
  - JavaScript
  - YAML
```

## Dictionaries (Mappings):

Use a colon : followed by a space to define key-value pairs.

Example:
```yaml
person:
  name: "Jane"
  age: 25
```

## Inline Format:

Lists and dictionaries can also be written inline:

```yaml
languages: [Python, JavaScript, YAML]
person: {name: "Jane", age: 25}
```

## Scalars:

Scalar values are simple data types like strings, numbers, booleans, etc.

```yaml
message: "Hello, YAML!"
count: 42
is_active: true
empty_value: null
```

# Advanced YAML Features

## Multiple Documents:
Separate multiple YAML documents in a single file using ---.

```yaml
--- # Document 1
name: "John"
---
name: "Jane"
```

## References (& and ):

Define a block of data with &, and refer to it later using *
.
Example:
```yaml
defaults: &defaults
  adapter: postgres
  host: localhost

development:
  database: myapp_development
  <<: *defaults
```

Result: development inherits the values from defaults.

## Literal Block Scalar (|):

Keeps newlines and preserves the text as-is.

Example:
```yaml
description: |
  This is a multi-line
  description with newlines.
```

## Folded Block Scalar (>):

Converts newlines into spaces.

Example:
```yaml
description: >
  This is a folded
  text block.
```

Result: "This is a folded text block."

## Custom Tags (!):
Tags allow you to attach metadata to YAML elements.

Example:
```yaml
!tagged
data: "example"
```

## Simple List:

```yaml
languages:
  - Python
  - JavaScript
  - YAML
```

## Key-Value Pairs:

```yaml
person:
  name: "Jane"
  age: 25
  skills:
    - coding
    - design

```

## Mapping Scalars to Scalars:

```yaml
metrics:
  height: "6'2"
  weight: 90
  BMI: 28

```

## Mapping Scalars to Sequences:

```yaml
categories:
  sports:
    - Cricket
    - Football
  technology:
    - AI
    - Blockchain

```
## Nested Structures:

```yaml
school:
  name: "ABC High School"
  address:
    street: "123 Elm St"
    city: "Metropolis"
  students:
    - name: "Alice"
      age: 14
    - name: "Bob"
      age: 15
```

#### YAML vs JSON

YAML is more human-readable compared to JSON. Here’s the same data in both formats:

JSON:
```json
{
  "name": "Jane",
  "age": 25,
  "skills": ["coding", "design"]
}
```


YAML:
```yaml
name: "Jane"
age: 25
skills:
  - coding
  - design
```

## Common Mistakes to Avoid

Using Tabs: Use spaces for indentation, not tabs.
Missing Space After Colon: Always leave a space after :.
    Correct: name: "Jane"
    Incorrect: name:"Jane"
Inconsistent Indentation: All items at the same level must have the same indentation.

With this understanding, you should be able to read, write, and debug YAML files effectively!

## Ansible Modules Overview
Ansible modules are the core components that perform specific tasks in a playbook. They are reusable, standalone scripts designed to automate tasks on remote systems. Here's a breakdown:

### General Characteristics

**Purpose**: Modules perform actions like managing files, configuring services, installing packages, and interacting with cloud platforms.
**Idempotency**: They ensure that tasks achieve a consistent state. For example, if a service is already started, running the task again will not restart it unnecessarily.
**Language**: Modules return JSON, so they can be written in any programming language.
**Integration**: Modules trigger "change events" that notify handlers to execute additional tasks when changes occur.
**Documentation**: You can access details about modules using the ansible-doc command:
**ansible-doc yum**: Displays documentation for the yum module.
**ansible-doc -l**: Lists all available modules.

### Using Modules
- Command-line Usage:
	Execute modules directly:

```yaml
ansible webservers -m service -a "name=httpd state=started"
```
Examples:

    ping: Checks connectivity with hosts.
    command: Runs a specific command (e.g., reboot).
    service: Manages services.

- Complex Arguments (YAML Syntax):
Instead of passing arguments inline, YAML syntax makes tasks more readable:
```yaml
- name: Restart webserver
  service:
    name: httpd
    state: restarted
```

### Types of Modules

Ansible modules are categorized based on their functionality. Below are common types and their examples:

**File Modules**
    Purpose: Manage files and directories.
    Examples: copy, fetch, file, template.
    Use Case:
        Copy files from a control node to target systems.
        Set file permissions.
        Create symbolic links.

**Package Management Modules**
    Purpose: Handle software package management across platforms.
    Examples: yum, apt, dnf, pip, gem, npm.
    Use Case: Install, update, or remove software.

**Service Modules**
    Purpose: Manage services on systems.
    Examples: service, systemd.
    Use Case: Start, stop, restart, or enable/disable services at boot.

**User and Group Management Modules**
    Purpose: Manage user accounts and groups.
    Examples: user, group.
    Use Case: Add or modify users/groups or set passwords.

**Networking Modules**
    Purpose: Configure networking devices and services.
    Examples: uri, ios_config, net_get.
    Use Case: Configure network interfaces or fetch HTTP data.

**Cloud Modules**
    Purpose: Work with cloud providers.
    Examples: ec2 (AWS), azure_rm (Azure), gcp_compute (GCP).
    Use Case: Provision, manage, and delete cloud resources (VMs, storage, etc.).

**Database Modules**
    Purpose: Manage databases and database users.
    Examples: mysql_db, postgresql_user.
    Use Case: Create or delete databases, users, or permissions.

**System Info and Setup Modules**
    Purpose: Gather system facts or configure basic system settings.
    Examples: setup, hostname.
    Use Case: Collect system information or set up hostname/timezone.

**Security Modules**
    Purpose: Configure security policies.
    Examples: firewalld, seboolean, selinux.
    Use Case: Manage firewalls, SELinux, or other security settings.

**Command and Shell Modules**
    Purpose: Run commands on target systems.
    Examples: command, shell, raw.
    Use Case: Execute commands directly (not recommended for idempotent tasks).

### Examples

1. Restart a Service
```yaml
- name: Restart nginx service
  service:
    name: nginx
    state: restarted
```

2. Install a Package
```yaml
- name: Install nginx
  yum:
    name: nginx
    state: present
```

3. Create a User
```yaml
- name: Add a user
  user:
    name: johndoe
    state: present
```

4. Copy a File
```yaml
- name: Copy configuration file
  copy:
    src: /path/to/local/file.conf
    dest: /etc/service/config.conf
    mode: '0644'
```

Ansible modules simplify automation tasks, ensuring flexibility, readability, and maintainability across various environments.

### **Ansible Inventory Files Overview**

Inventory files in Ansible specify the hosts (target machines) and organize them into logical groups to efficiently manage configurations and tasks. They also allow setting variables at both group and host levels for more granular control.
### **Key Components**

#### **Hosts**

- Hosts are the target systems managed by Ansible.
- They can be identified using:
    - **IP addresses**: `192.168.1.10`
    - **Hostnames**: `webserver1`
    - **Domain names**: `web1.example.com`

#### **Groups**

- **Purpose**: Organize hosts into logical collections.
    - Examples: `web_servers`, `databases`, `staging`.
- **Benefits**:
    - Makes it easier to apply tasks to subsets of hosts.
    - Supports **nested groups**, enabling hierarchical structures.
        - Example: A group `all` can have subgroups `web_servers` and `databases`.

#### **Variables**

Variables allow you to define host-specific or group-wide configurations.

1. **Group Variables**:
    
    - Applied to all hosts in a group.
    - Defined under `[group_name:vars]` in the inventory file.

Example:
```yaml
[web_servers:vars]
ansible_user=ubuntu
ansible_port=22
```

2. **Host Variables**:

    Applied to a single host.
    Useful for host-specific settings like custom paths or IPs.
    
Example:
```yaml
web1.example.com ansible_user=ubuntu ansible_host=192.168.1.10
```

## Static Inventory

A static inventory is a simple file that explicitly lists hosts and groups. It can be written in INI or YAML format.
INI Format

Default format for static inventories.
Uses sections to define groups and variables.

Example:
```yaml
[web_servers]
web1.example.com ansible_user=ubuntu
web2.example.com ansible_user=ubuntu

[databases]
db1.example.com ansible_user=db_admin
```

YAML Format

Structured and more readable.
Useful for complex inventories.

Example:
```yaml
all:
  hosts:
    localhost:
      ansible_connection: local
  children:
    web_servers:
      hosts:
        web1.example.com:
          ansible_user: ubuntu
        web2.example.com:
          ansible_user: ubuntu
    databases:
      hosts:
        db1.example.com:
          ansible_user: db_admin
```

## Dynamic Inventory

A dynamic inventory generates the list of hosts and variables programmatically, suitable for environments with frequent changes (e.g., cloud setups).

- Dynamic Sources: Cloud providers (AWS, Azure, GCP), Kubernetes clusters, etc.
- Implementation:
    - Use inventory scripts or plugins to fetch and generate data in JSON or YAML format.
- Examples:
    - AWS EC2 plugin (aws_ec2): Retrieves instances from AWS.
    - GCP Compute plugin (gcp_compute): Retrieves VMs from Google Cloud.
- Configuration:
    - Point Ansible to the plugin or script in ansible.cfg or playbooks.

## Patterns

Ansible allows targeting hosts using patterns:

- Groups:
        Example: ansible-playbook -i inventory.ini playbook.yml -l web_servers
- Wildcards:
        Example: web* targets web1, web2, etc.
- Combined Patterns:
        web_servers:databases targets both web_servers and databases.

Examples

1. Static Inventory (INI Format)
```yaml
[web_servers]
web1.example.com ansible_user=ubuntu
web2.example.com ansible_user=ubuntu

[databases]
db1.example.com ansible_user=db_admin

[all:children]
web_servers
databases
```

2. Static Inventory (YAML Format)
```yaml
all:
  hosts:
    localhost:
      ansible_connection: local
  children:
    web_servers:
      hosts:
        web1.example.com:
          ansible_user: ubuntu
        web2.example.com:
          ansible_user: ubuntu
    databases:
      hosts:
        db1.example.com:
          ansible_user: db_admin
```

3. Dynamic Inventory
- Example with AWS EC2 plugin:
```yaml
plugin: aws_ec2
regions:
  - us-east-1
keyed_groups:
  - key: tags.Name
filters:
  tag:Environment: Production
```

## Ansible Playbooks Overview

Ansible playbooks are YAML files that define a sequence of tasks for managing configurations, deploying applications, or orchestrating operations across target machines. Playbooks consist of plays, each targeting specific hosts or groups and containing tasks to be executed.
Components of Ansible Playbooks

1. Plays

    A play is a set of tasks that operate on a specific group of hosts.
    Playbooks can have one or multiple plays, each targeting different groups or servers.

2. Hosts

    Define the target machines for each play using host groups (e.g., webservers or all) from the inventory file.

3. Tasks

    Each task uses an Ansible module (e.g., yum, service, copy) to perform an action on the target machines.

4. Variables

    Variables provide flexibility, allowing reusable and customizable configurations. They are defined at the play or task level.

5. Handlers

    Handlers are special tasks triggered using the notify directive. They typically manage system changes, such as restarting a service after a configuration update.

6. Conditionals and Loops

    Add dynamic behavior by executing tasks conditionally or repeating tasks over a list of values.

## Playbook 1: Configure a Web Server
Playbook Content

```yaml
---
- name: Configure a web server
  hosts: webservers
  become: true  # Run tasks with elevated privileges (e.g., sudo)

  vars:
    http_port: 80
    document_root: /var/www/html

  tasks:
    - name: Install Apache
      yum:
        name: httpd
        state: present

    - name: Start and enable Apache
      service:
        name: httpd
        state: started
        enabled: true

    - name: Copy index.html to the document root
      copy:
        src: files/index.html
        dest: "{{ document_root }}/index.html"
        mode: '0644'

  handlers:
    - name: Restart Apache
      service:
        name: httpd
        state: restarted

```
### Explanation

1. Play:
        Targets the webservers group defined in the inventory file.
        Uses become: true to run tasks as a privileged user (root or sudo).

2. Variables:
        http_port: Specifies the HTTP port (default 80).
        document_root: Defines the path for the web server's document root.

3. Tasks:
        Install Apache:
            Uses the yum module to ensure Apache (httpd) is installed.
            state: present ensures the package is installed but doesn’t reinstall if already installed.
        Start and Enable Apache:
            The service module ensures the httpd service is running and enabled to start on boot.
        Copy index.html:
            Copies a file from the files/index.html in your Ansible control node to the document_root on the managed nodes.
            mode: '0644' sets the file permissions.

4. Handlers:
        Restart Apache:
			- A handler to restart the Apache service.
            - Not triggered in this playbook but is defined for future tasks that might notify it.

**Usage**:

```yaml
ansible-playbook webserver.yml -i inventory
```
- Runs the playbook on hosts in the webservers group.

## Playbook 2: Configure System Basics
Playbook Content

```yaml
- name: Configure system basics
  hosts: all
  become: true  # Run tasks as root

  vars:
    new_user: ansible_user
    packages:
      - vim
      - curl
      - git

  tasks:
    - name: Create a new user
      user:
        name: "{{ new_user }}"
        state: present
        groups: sudo
        shell: /bin/bash

    - name: Install essential packages
      yum:
        name: "{{ item }}"
        state: present
      loop: "{{ packages }}"

    - name: Open HTTP port in firewall
      firewalld:
        port: 80/tcp
        permanent: true
        state: enabled
        immediate: true

    - name: Reload firewalld to apply changes
      service:
        name: firewalld
        state: reloaded

```
### Explanation

**Play**:
- Targets all hosts (hosts: all) from the inventory.
- become: true ensures tasks are executed with root privileges.

**Variables**:
- new_user: Specifies the name of the new user to be created.
- packages: Lists essential packages (vim, curl, git) to install. 

**Tasks**:
**Create a New User**:
- Uses the user module to create a user (ansible_user).
- Adds the user to the sudo group and sets their shell to /bin/bash.
**Install Essential Packages**:
- Uses the yum module with loop to iterate over the list of packages (vim, curl, git) and installs them.
**Open HTTP Port in Firewall**:
- Uses the firewalld module to open port 80 (HTTP) for incoming traffic.
- permanent: true ensures the change persists after reboots.
- immediate: true applies the change immediately.
**Reload Firewall**:
- Reloads the firewalld service to apply the new rules.

**Usage**:

```yaml
ansible-playbook system_basics.yml -i inventory
```

- Runs the playbook on all hosts listed in the inventory.


## Playbook 3 - Deploy Node.js application

```yaml
---
- name: Configure a web server
  hosts: webservers
  become: true  # Run tasks with elevated privileges (e.g., sudo)

  vars:
    http_port: 80
    document_root: /var/www/html

  tasks:
    - name: Install Apache
      yum:
        name: httpd
        state: present

    - name: Start and enable Apache
      service:
        name: httpd
        state: started
        enabled: true

    - name: Copy index.html to the document root
      copy:
        src: files/index.html
        dest: "{{ document_root }}/index.html"
        mode: '0644'

  handlers:
    - name: Restart Apache
      service:
        name: httpd
        state: restarted

```

### Explanation

1. Play:
    - Targets the app_servers group defined in the inventory file.
    - Runs tasks as a privileged user (become: true).

2. Variables:
    - repo_url: The Git repository URL for the application.
    - app_dir: Directory on the target system where the application will be deployed.

3. Tasks:
    - Ensure Node.js is Installed:
            Uses the yum module to install Node.js from the system's package manager.
    - Clone the Application Repository:
            Uses the git module to clone the repository from repo_url into the directory specified by app_dir.
            version: main: Ensures the main branch is used.
            force: yes: Ensures the repository is updated even if it already exists.
    - Install npm Dependencies:
            Uses the npm module to install or update all dependencies listed in the application's package.json.
            state: latest: Ensures the latest versions are installed.
    - Start the Application:
            Uses the command module to run the application with Node.js.
            async: 30: Runs the command asynchronously and allows up to 30 seconds for it to finish.
            poll: 0: The task starts the application in the background and does not wait for completion.

## Playbook 4: Setup MySQL Database

```yaml
---
- name: Setup MySQL Database
  hosts: db_servers
  become: true

  vars:
    mysql_root_password: "rootpassword"
    db_name: "my_database"
    db_user: "db_user"
    db_password: "db_password"

  tasks:
    - name: Install MySQL
      yum:
        name: mysql-server
        state: present

    - name: Start and enable MySQL
      service:
        name: mysqld
        state: started
        enabled: true

    - name: Set MySQL root password
      mysql_user:
        name: root
        host: localhost
        password: "{{ mysql_root_password }}"
        check_implicit_admin: true

    - name: Create a new database
      mysql_db:
        name: "{{ db_name }}"
        state: present

    - name: Create a new MySQL user
      mysql_user:
        name: "{{ db_user }}"
        password: "{{ db_password }}"
        priv: "{{ db_name }}.*:ALL"
        state: present

```
### Explanation

1. Play:
    - Targets the db_servers group defined in the inventory file.
    - Executes tasks with elevated privileges (become: true).

2. Variables:
    - mysql_root_password: Root password for the MySQL database.
    - db_name: Name of the database to be created.
    - db_user: New MySQL user to be created.
    - db_password: Password for the new MySQL user.

3. Tasks:
    - Install MySQL:
            Uses the yum module to install the mysql-server package.
    - Start and Enable MySQL:
            Uses the service module to start the MySQL service (mysqld) and enable it to start on boot.
    - Set MySQL Root Password:
            Uses the mysql_user module to set the root user's password.
            check_implicit_admin: true: Ensures the task works even if the root account doesn't initially require a password.
    - Create a New Database:
            Uses the mysql_db module to create a database with the name specified in db_name.
    - Create a New MySQL User:
            Uses the mysql_user module to create a user with the credentials defined in db_user and db_password.
            priv: "{{ db_name }}.*:ALL": Grants all privileges on the specified database to the user.

### Usage
### Deploy Node.js Application
```yaml
ansible-playbook deploy_nodejs.yml -i inventory
```
### Setup MySQL Database

```yaml
ansible-playbook setup_mysql.yml -i inventory
```

# Ansible Roles: A Detailed Explanation

Ansible roles are a powerful feature that allows you to organize your automation tasks into reusable and modular components. By grouping related tasks, variables, files, templates, and handlers into a standardized directory structure, roles enhance maintainability and shareability in automation projects.
Directory Structure


```yaml
ansible-playbook -i inventory site.yml #used to create the directory structure for my_role
```

When you create a role, it follows a well-defined directory structure:

```plaintext
my_role/
├── defaults/           # Default variables (lowest precedence)
│   └── main.yml
├── vars/               # Role-specific variables (higher precedence than defaults)
│   └── main.yml
├── files/              # Static files to copy to the managed hosts
├── templates/          # Jinja2 templates to dynamically generate configuration files
├── tasks/              # Main tasks file and additional task files
│   └── main.yml
├── handlers/           # Handlers triggered by notify actions
│   └── main.yml
├── meta/               # Role metadata (dependencies, etc.)
│   └── main.yml
└── README.md           # Documentation for the role

```
### Purpose of Each Directory

1. defaults/:
    - Stores default variables with the lowest precedence in the variable hierarchy.
    - Example: Common settings like document_root or service_name are defined here.

2. vars/:
    - Contains variables with higher precedence than defaults.
    - Ideal for variables specific to the role or environment.

3. files/:
    - Holds static files to be copied to the managed nodes.
    - Example: index.html for a web server.

4. templates/:
    - Contains Jinja2 templates for dynamically rendering configuration files.
    - Example: Apache’s httpd.conf.j2.

5. tasks/:
    - Central to the role, this directory contains the main.yml file where tasks are defined.
    - Additional task files can be included for modularity.

6. handlers/:
    - Defines actions triggered by other tasks.
    - Example: Restarting a service after applying a configuration change.

7. meta/:
    - Stores metadata about the role, such as dependencies on other roles.
    - Ensures prerequisite roles are executed first.

8. README.md:
    - Documents the role’s purpose, usage, and any additional instructions.

### Example Role: Apache
#### Objective:
This role installs Apache, sets up an index page, configures Apache, and ensures the service is started.
### defaults/main.yml

- Defines default variables for the role.

```yaml
# apache/defaults/main.yml
document_root: /var/www/html
service_name: httpd

files/index.html

A static HTML file to be copied to the server.

<!-- apache/files/index.html -->
<html>
  <body>
    <h1>Welcome to Apache Web Server</h1>
  </body>
</html>

```
### templates/httpd.conf.j2
- A Jinja2 template for Apache’s configuration file, using variables defined in the role.

```yaml
# apache/templates/httpd.conf.j2
<VirtualHost *:80>
    DocumentRoot "{{ document_root }}"
    <Directory "{{ document_root }}">
        AllowOverride None
        Require all granted
    </Directory>
</VirtualHost>
```
### handlers/main.yml
- Defines a handler to restart Apache if configuration files are updated.

```yaml
# apache/handlers/main.yml
- name: Restart Apache
  service:
    name: "{{ service_name }}"
    state: restarted
```
### tasks/main.yml

**Main tasks for the role.**

```yaml
# apache/tasks/main.yml
- name: Install Apache
  yum:
    name: "{{ service_name }}"
    state: present

- name: Copy index.html to document root
  copy:
    src: index.html
    dest: "{{ document_root }}/index.html"
    mode: '0644'

- name: Copy Apache configuration
  template:
    src: httpd.conf.j2
    dest: /etc/httpd/conf/httpd.conf
    mode: '0644'
  notify: Restart Apache

- name: Start and enable Apache service
  service:
    name: "{{ service_name }}"
    state: started
    enabled: true

```
### Using the Role

To use the apache role in a playbook:
Playbook: site.yml

```yaml
# site.yml
- name: Configure Apache Web Server
  hosts: webservers
  become: true

  roles:
    - apache

```
#### Run the Playbook

```yaml
ansible-playbook -i inventory site.yml
```
### Role Dependencies

Roles can declare dependencies in their meta/main.yml. If the apache role requires another role (e.g., common), specify it as follows:
meta/main.yml

```yaml
#  apache/meta/main.yml
dependencies:
  - role: common
```

When the apache role is executed, the common role will automatically run first.
### Key Features of Roles
1. Reusability:
    - Roles can be reused across multiple projects and teams, saving time and effort.
2. Modular Design:
    - Each role encapsulates a specific set of functionality.
3. Readability:
    - Playbooks become cleaner and more concise by referencing roles.

### Best Practices

1. Descriptive Role Names:
	-  Use meaningful names (e.g., webserver instead of apache).
2. Avoid Hardcoding:
    - Define variables in defaults or vars for flexibility.
3. Self-Contained Roles:
    - Ensure roles are independent and modular.
4. Selective Execution:
    - Use tags to selectively execute tasks within roles.

### Advantages of Using Roles

- Organized Structure: Helps manage complex playbooks by grouping related components.
- Scalability: Makes it easy to scale automation tasks across large environments.
- Maintainability: Simplifies updates and modifications by isolating functionality.

By following the role structure and best practices, Ansible automation becomes highly efficient, reusable, and maintainable.

# Ansible Ad-Hoc Commands: A Detailed Overview

Ad-hoc commands are lightweight, one-off commands used in Ansible for performing tasks quickly without the overhead of writing a playbook. They are especially useful for quick checks, configurations, and administrative tasks.

### General Syntax

```yaml
ansible <host-pattern> -m <module> -a "<module options>"
```

```plaintext
<host-pattern>: Specifies target hosts or groups in the inventory.
-m <module>: Indicates the Ansible module to use (e.g., ping, copy, yum).
-a"<module options>": Provides arguments or options for the module.
```

### Common Use Cases
1. Checking Connectivity
	- Tests the connection between Ansible and remote hosts.
	- Uses the ping module, which verifies Python availability on the host (not ICMP-based).

2. Gathering System Information
    - The setup module gathers detailed system facts (e.g., OS, CPU, memory).
    - With filtering, you can retrieve specific facts such as ansible_interfaces.

3. Installing or Removing Packages

- **For CentOS/RHEL:**
```yaml
ansible webservers -m yum -a "name=httpd state=present"
```

- **For Ubuntu/Debian:**
```yaml
ansible webservers -m apt -a "name=apache2 state=present"
```

- Installs httpd or apache2 on all hosts in the webservers group.
- Use state=absent to remove packages.

4. Managing Services

- **Start a service:**
```yaml
ansible webservers -m service -a "name=httpd state=started"
```

- **Enable a service on boot:**
```yaml
ansible webservers -m service -a "name=httpd enabled=yes"
```

- **Restart a service:**
```yaml
ansible webservers -m service -a "name=httpd state=restarted"
```

5. Copying Files

```yaml
ansible all -m copy -a "src=/path/to/local/file dest=/path/to/remote/file mode=0644"
```

- Transfers files from the control node to remote hosts.
- Sets file permissions using the mode parameter.

6. Executing Commands

- Run a command using the command module:

```yaml
ansible all -m command -a "uptime"
```

- Run a shell command (e.g., with pipes):

```yaml
ansible all -m shell -a "echo 'Hello, Ansible!' >> /tmp/hello.txt"
```

- Use shell sparingly as it bypasses Ansible's safety mechanisms.

7. Managing Users and Groups

- Create a new user:

```yaml
ansible all -m user -a "name=johndoe state=present"
```

- Set a hashed password for a user:

```yaml
ansible all -m user -a "name=johndoe password={{ 'password' | password_hash('sha512') }}"
```

- Create a group:

```yaml
ansible all -m group -a "name=developers state=present"
```

8. Checking Disk Space or Memory

- Check disk space:

```yaml
ansible all -m command -a "df -h"
```

- Check memory usage:

```yaml
ansible all -m command -a "free -m"
```

9. Rebooting Hosts

```yaml
ansible all -m reboot
```

- Safely reboots remote systems.

Additional Options

1. Run as a Different User:

```yaml
ansible all -m ping -u username
```

2. Use Sudo Privileges:

```yaml
ansible all -m yum -a "name=httpd state=present" --become
```

3. Specify a Custom Inventory File:

```yaml
ansible all -m ping -i custom_inventory
```

When to Use Ad-Hoc Commands vs. Playbooks?

![[Pasted image 20241117010034.png]]



