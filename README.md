# 🚀 Ansible Role: install-docker

Esta role instala o **Docker** em servidores Linux e configura automaticamente um cluster **Docker Swarm**, com 1 manager e múltiplos workers.

---

## 📂 Estrutura do projeto

```
roles/install-docker/
├── defaults/
│   └── main.yml
├── tasks/
│   ├── main.yml
│   ├── swarm_init.yml
│   └── swarm_join.yml
└── meta/
    └── main.yml
```

---

## ⚙️ Requisitos

- Python 3 no host
- Módulos Ansible:
  - [`community.docker`](https://docs.ansible.com/ansible/latest/collections/community/docker/index.html)

Instale a collection caso ainda não tenha:

```bash
ansible-galaxy collection install community.docker
```

---

## 📌 Inventário de exemplo

`inventory/hosts.ini`:
```ini
[manager]
node01 ansible_host=192.168.18.98

[workers]
node02 ansible_host=192.168.18.99
node03 ansible_host=192.168.18.97

[docker:children]
manager
workers
```

---

## ▶️ Playbook de exemplo

`playbooks/site.yml`:
```yaml
- hosts: docker
  become: true
  roles:
    - install-docker
```

---

## 🚀 Como usar

1. Ajuste os hosts no inventário (`inventory/hosts.ini`).
2. Execute o playbook:

```bash
ansible-playbook -i inventory/hosts.ini playbooks/site.yml
```

---

## 📖 O que a role faz

- Atualiza o cache do APT.
- Instala pacotes necessários.
- Instala o Docker.
- Inicializa o **Docker Swarm** no `manager`.
- Obtém o token de join.
- Junta automaticamente os `workers` ao cluster.

---

## 📝 Notas

- Caso queira adicionar novos **managers** ou **workers** no futuro, basta atualizar o inventário e rodar o playbook novamente.
- Certifique-se de que as portas necessárias do Swarm estão liberadas:
  - `2377/tcp` (cluster management)
  - `7946/tcp` e `7946/udp` (comunicação interna)
  - `4789/udp` (overlay network)
