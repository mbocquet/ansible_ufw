Ansible UFW role.

Ansible role to install UFW (Uncomplicated FireWall) and manage firewall rules.

# Requirements

None.

# Role Variables

See defaults/main.yml for details

# Dependencies

None.

# Install this role as submodule in a git repository

`git submodule add https://git.sekoya.org/mb/ansible_ufw.git roles/ufw`

# Example Playbook

    - hosts: servers
      gather_facts: false
      roles:
        - role: ufw
          when: ufw_rules is defined


    - hosts: servers
      gather_facts: false
      roles:
        - role: ufw
          ufw_rules:
            # Enable UFW with a default deny policy
            - state: enabled
              policy: deny
            # Allow all outbound traffic
            - direction: outgoing
              default: allow
            # Allow port forwarding
            - direction: routed
              default: allow
            # SSH
            - rule: allow
              name: SSH
            # Allow link-local IPv6 addresses to local TCP ports
            - rule: allow
              src: fe80::/64
              port: 80,8000,9090
              proto: tcp
            # If more ports to the same rule is added, rule should be deleted
            # and another one added
            # Delete previous rule
            - rule: allow
              src: fe80::/64
              port: 80,8000,9090
              proto: tcp
              delete: true
            # Then add more ports
            - rule: allow
              src: fe80::/64
              port: 80,8000,9090,6000
              proto: tcp

# License

GPLv3

# Author Information

http://www.sekoya.org
