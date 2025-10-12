# Playbook Ansible para Implantar n8n com Docker

Este playbook Ansible automatiza a implantação da ferramenta de automação de fluxos de trabalho [n8n](https://n8n.io/) num servidor Ubuntu remoto. O script trata de todos os passos necessários: atualizar o servidor, instalar o Docker e o Docker Compose, e implantar o n8n usando um ficheiro `docker-compose.yml`.

---

## Requisitos

* **Python 3 & venv**: Deve estar instalado na sua máquina local.
* **Servidor de Destino**: Um contentor ou servidor Ubuntu em execução.
* **Acesso SSH**: Deve ter autenticação baseada em chave SSH configurada para aceder ao servidor de destino com um utilizador que tenha privilégios `sudo`.

---

## Estrutura de Ficheiros

Garanta que o seu diretório de projeto está estruturado da seguinte forma:
```bash
├── README.md
├── cleanup_n8n.yml
├── deploy_n8n.yml
├── files
│   └── docker-compose.yml
├── inventory-template.ini
└── requirements.txt
```

---

## Configuração do Ambiente Local

Antes de executar o playbook, precisa de configurar um ambiente virtual Python local para gerir as dependências.

1.  **Criar o Ambiente Virtual**:
    A partir do diretório raiz do projeto, execute:
    ```bash
    python3 -m venv .venv
    ```

2.  **Ativar o Ambiente**:
    ```bash
    source .venv/bin/activate
    ```
    *(O seu terminal deverá agora mostrar o prefixo `(.venv)`)*

3.  **Instalar o Ansible e as Dependências**:
    ```bash
    pip install -r requirements.txt
    ```

---

## Configuração do Servidor

Agora, configure o ficheiro `inventory.ini` com os detalhes do seu servidor.

1.  Abra o `inventory.ini`.
2.  Substitua os valores de exemplo:
    * `x.x.x.x`: O endereço IP do seu servidor de destino.
    * `your_ssh_user`: O nome de utilizador para a ligação SSH (ex: `ubuntu`, `root`).
    * `/path/to/your/private_key`: O caminho absoluto para a sua chave privada SSH na sua máquina local.

**Exemplo de `inventory.ini`:**

```ini
[n8n_server]
n8n-01 ansible_host=x.x.x.x

[n8n_server:vars]
ansible_user=ubuntu
ansible_python_interpreter=/usr/bin/python3
ansible_ssh_private_key_file=/home/user/.ssh/id_rsa
```

ansible-playbook -i inventory.ini deploy_n8n.yml
ansible-playbook -i inventory.ini deploy_n8n.yml --step #Se quer assistir cada step