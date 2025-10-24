# Instalação rápida

## Instalando os componentes centrais do Wazuh

Você pode instalar o indexador Wazuh, o servidor Wazuh e o painel Wazuh em um único host ou distribuí-los em configurações de cluster. Cada componente central do Wazuh suporta dois métodos de instalação, e ambos fornecem instruções para instalar os componentes centrais em um único host ou em hosts separados.

A maneira mais rápida de instalar o Wazuh e colocar os componentes centrais em funcionamento é realizando uma instalação completa como segue abaixo:  

1. Baixe e execute o assistente de instalação do Wazuh.

    ```bash
    curl -sO https://packages.wazuh.com/4.13/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
    ```

    Assim que o assistente concluir a instalação, a saída mostrará as credenciais de acesso e uma mensagem que confirma que a instalação foi bem-sucedida.

    ```bash
    INFO: --- Summary ---
    INFO: You can access the web interface https://<WAZUH_DASHBOARD_IP_ADDRESS>
        User: admin
        Password: <ADMIN_PASSWORD>
    INFO: Installation finished.
    ```

    Agora você instalou e configurou o Wazuh.  

2. Acesse a interface web do Wazuh com

`https://<WAZUH_DASHBOARD_IP_ADDRESS>` e suas credenciais:

* Nome de usuário: `admin`  

* Senha: `<ADMIN_PASSWORD>`  

Ao acessar o painel do Wazuh pela primeira vez, o navegador exibe uma mensagem de aviso informando que o certificado não foi emitido por uma autoridade confiável. Isso é esperado e o usuário tem a opção de aceitar o certificado como exceção ou, alternativamente, configurar o sistema para usar um certificado de uma autoridade confiável.

**Observacao:** *Você pode encontrar as senhas de todos os usuários do indexador Wazuh e da API Wazuh no* `wazuh-passwords.txt` *arquivo dentro do* `wazuh-install-files.tar`*. Para imprimi-las, execute o seguinte comando:*

```bash
sudo tar -O -xvf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt
```

Se você quiser desinstalar os componentes centrais do Wazuh, execute o assistente de instalação do Wazuh usando a opção `-u` ou `--uninstall`.

### Observação

**Ação recomendada:** desabilitar atualizações do Wazuh.

Recomendamos desabilitar os repositórios de pacotes Wazuh após a instalação para evitar atualizações acidentais que podem danificar o ambiente.

Execute o seguinte comando para desabilitar o repositório Wazuh:

#### APT (Debian/Ubuntu)

```bash
# sed -i "s/^deb /#deb /" /etc/apt/sources.list.d/wazuh.list
# apt update
```

### Próximos passos

Agora que a instalação do Wazuh está pronta, você pode começar a implantar o agente Wazuh. Ele pode ser usado para proteger laptops, desktops, servidores, instâncias de nuvem, contêineres ou máquinas virtuais. O agente é leve e multifuncional, oferecendo uma variedade de recursos de segurança.

**Aviso**
O suporte para os seguintes sistemas operacionais termina no Wazuh 5.0.0: Red Hat 5, CentOS 5, Oracle Linux 5, SUSE Linux Enterprise Server 11, Windows XP, Windows Vista, Windows Server 2003, Solaris, AIX e HP-UX.
___
[< Agente Wazuh](Wazuh_Agent.md "Wazuh Agent")  
[Guia de Instalação >](Installation_guide.md "Requisitos Indexador")  
