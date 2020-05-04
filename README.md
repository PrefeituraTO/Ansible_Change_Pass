# Ansible_Change_Pass
Alterar a senha de root dos servidores Linux/PFSense

# Requisitos:
  * Ansible: 2.9.2 ou mais novo;
  * OpenSSL: 1.1.1g-1 ou mais novo;
	
# Modo de usar:
  1. Clonar repositório
  2. Adicionar os IPs/nomes dos Hosts no arquivo `hosts`
  3. Configurar os acessos no arquivo .ssh/config (arquivo em anexo no diretorio `extras`)
  4. Criptografar a nova senha com openssl:
  > Caso a senha contenha o caracter `#` é necessário utilizar a barra invertida antes do caracter para "escapar" a interpretação do caratere # como comentário.
``` bash
	diego@PCPD033777:~$ openssl passwd -1 -salt xyz \#N0vas3nh4
    $1$xyz$Kt4Urun/SCrFEMqgr5eS31
```
  
  5. Adicione o valor correspondente no arquivo `group_vars/all.yml` como valor para a variável `root_password`
``` bash
	root_password: $1$xyz$Kt4Urun/SCrFEMqgr5eS31
```
  6. Execute o playbook do ansible:
``` bash
	 diego@PCPD033777:~$ ansible-playbook -i hosts main.yml
``` 