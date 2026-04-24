# Ansible EC2 Automation Project

## Step-by-Step Process

This project demonstrates basic infrastructure automation using Ansible with an AWS EC2 instance.

It automates:
  - Creating a directory on remote server
  - Creating a file inside the directory
  - Writing content into the file
  - Displaying the output directly after execution

This simulates how configuration management works in real DevOps environments.

## Project Overview
 - Remote server (EC2) is managed using Ansible
 - Folder and file creation is fully automated
 - File content is managed using Ansible modules
 - No need to manually log into the server
 - Output is displayed directly in terminal

## Technologies Used
  - Ansible
  - AWS (EC2 Instance)
  - YAML (Playbooks)

## Project Structure
```
      ansible-project/
           |
           ├── inventory.ini
           ├── playbook.yml
           └── README.md
```

## Inventory File (inventory.ini)
```
    [webserver]
    <ec2-public-ip>
    
    [webserver:vars]
    ansible_user=ubuntu
    ansible_ssh_private_key_file=~/test.pem
```

## Playbook (playbook.yml)
```
    ---
    - name: create folders and files in ec2
      hosts: all
    
      tasks:
        - name: create a folder
          file:
            path: /home/ubuntu/happy
            state: directory
    
        - name: create file and add content
          copy:
            dest: /home/ubuntu/happy/file.txt
            content: "Success, playbook is working.."
    
        - name: read file content
          shell: cat /home/ubuntu/happy/file.txt
          register: result
    
        - name: display output
          debug:
            var: result.stdout
```

## Process to Run the Project
1. Install Ansible (if not installed)
   ```
    sudo apt update
    sudo apt install ansible -y
   ```

2. Set Permissions for Key
   ```
   chmod 400 ~/test.pem
   ```

3. Test Connection
   ```
   ansible all -i inventory.ini -m ping
   ```

4. Run Playbook
   ```
   ansible-playbook -i inventory.ini playbook.yml
   ```

## Expected Output
After running the playbook, you will see:
```
"result.stdout": "Success, playbook is working.."
```

## Notes
  - Ensure EC2 instance is running
  - Port 22 (SSH) should be open in security group
  - Use correct private key path
  - Avoid spaces in folder names

## Key Learnings
  - Automating remote server tasks using Ansible
  - Writing YAML-based playbooks
  - Managing files and directories remotely
  - Using inventory for multiple servers
  - Eliminating manual server configuration
  - Understanding Infrastructure as Code (IaC)



