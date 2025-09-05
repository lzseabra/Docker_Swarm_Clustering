🚀 Ansible Role: install-docker
=========
Esta role instala o **Docker** em servidores Linux e configura automaticamente um cluster **Docker Swarm**, com 1 manager e múltiplos workers.

---

## 📂 Estrutura do projeto

roles/install-docker/
├── defaults/
│ └── main.yml
├── tasks/
│ ├── main.yml
│ ├── swarm_init.yml
│ └── swarm_join.yml
└── meta/
└── main.yml

# ⚙️ Requisitos
------------

- Python 3 no host
- Módulos Ansible:
  - [`community.docker`](https://docs.ansible.com/ansible/latest/collections/community/docker/index.html)

Instale a collection caso ainda não tenha:

```bash
ansible-galaxy collection install community.docker

invenory/hosts.ini:
-------------------
[manager]
node01 ansible_host=<Ajuste para o ip da rede>

[workers]
node02 ansible_host=<Ajuste para o ip da rede>
node03 ansible_host=<Ajuste para o ip da rede>

[docker:children]
manager
workers


Example Playbook
----------------

- hosts: docker
  become: true
  roles:
    - install-docker

🚀 Como usar
------------

ansible-playbook -i inventory/hosts.ini playbooks/site.yml


License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
# Docker_Swarm_Clustering

