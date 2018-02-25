# Deploy Metabase

Este projeto foi feito sob o visão de aprendizado. Não há fins comerciais em seu uso. Caso deseje, utilize-o e altere da forma que desejar.

## Definições do projeto

Aspectos, ferramentas e testes realizados durante o desenvolvimento deste script.

## Ansible - Ferramenta
Foi utilizada a ferramenta **Ansible** que permite abstrair o processo de execução de processos, independente do ambiente em que será executado, possibilitando e permitindo que pequenas alterações possibilitem a portabilidade para outras bases de Sistema Operacional.

## Conceitos

### Ambiente
Para testar e validar o script, foi utilizada a distribuição Linux **CentOS 7**, a mais utilizada em servidores.

Referência: http://searchdatacenter.techtarget.com/feature/Compare-popular-Linux-distributions-for-servers

### Ferramenta
Foi escolhida a ferramenta **Ansible**, devido ao fato de ter uma curva de aprendizado pequena, não necessita de grandes recursos de hardware, tem uma linguagem simplificda (YAML) e não necessita de um servidor para que possa funcionar.

Os únicos requisitos é que tenha um ambiente Linux para que a ferramenta seja instalada e configurada, podendo começar a utilizar imediatamente.

Em ambiente Windows a ferramenta ainda não opera corretamente.

## Como utilizar

### Instalação do Ansible
* Instale o Ansible em seu ambiente: ```yum install ansible```
    * Debian: ```apt install ansible -y```
    * RHEL: ```dnf install ansible -y```

### Preparando o ambiente para utilizar este projeto
```
sudo mkdir /etc/ansible/roles
sudo mkdir /etc/ansible/playbooks
cd /etc/ansible/roles
git clone git@github.com:vinicelms/desafio_1.git
sudo mv /etc/ansible/roles/desafio_1/metabase.yml /etc/ansible/playbooks
```

### Adicionando os hosts que o Ansible vai utilizar

Edite o arquivo de ```hosts``` do Ansible, localizado em ```/etc/ansible/hosts``` e adicione as informações do seu host:

```
[metabase]
IP_DO_SERVIDOR    ansible_user=USUARIO_PARA_LOGIN
```

Exemplo de como o arquivo de hosts deveria ficar:
```
[metabase]
192.168.0.5     ansible_user=viniciuscelms
```

### Executando o projeto para realizar o deploy do Metabase
```
cd /etc/ansible
ansible-playbook playbooks/metabase.yml -K
```

O parâmetro ```-K```, informa ao Ansible para para que requisite a senha de root, pois algumas **tasks** necessitarão de elevação de permissão.