# Guia de Instalação

## Instalação do Indexador (Instalação Assistida)

Instale e configure o indexador Wazuh como um cluster de nó único ou multinó em uma arquitetura de 64 bits (x86_64/AMD64 ou AARCH64/ARM64) usando o método de instalação assistida. O indexador Wazuh é um mecanismo de busca de texto completo altamente escalável. Ele oferece segurança avançada, alertas, gerenciamento de índice, análise aprofundada de desempenho e diversos outros recursos.

### Instalação do cluster do indexador Wazuh

O processo de instalação é dividido em três etapas.

1. Configuração inicial

2. Instalação de nós indexadores Wazuh

3. Inicialização do cluster

```markdown
    Observação: Você precisa de privilégios de usuário
    root para executar todos os comandos descritos abaixo.
```

#### Configuração inicial

Siga estas etapas para configurar sua implantação do Wazuh, criar certificados SSL para criptografar as comunicações entre os componentes do Wazuh e gerar senhas aleatórias para proteger sua instalação.

1. Baixe o assistente de instalação do Wazuh e o arquivo de configuração.  

    ```bash
        curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
        curl -sO https://packages.wazuh.com/4.14/config.yml
    ```

2. Edite ./config.ymle substitua os nomes dos nós e os valores de IP pelos nomes e endereços IP correspondentes. Você precisa fazer isso para todos os nós do servidor Wazuh, do indexador Wazuh e do painel Wazuh. Adicione quantos campos de nó forem necessários.  

    ```yaml
        nodes:
        # Wazuh indexer nodes
        indexer:
            - name: node-1
            ip: "<indexer-node-ip>"
            #- name: node-2
            #  ip: "<indexer-node-ip>"
            #- name: node-3
            #  ip: "<indexer-node-ip>"

        # Wazuh server nodes
        # If there is more than one Wazuh server
        # node, each one must have a node_type
        server:
            - name: wazuh-1
            ip: "<wazuh-manager-ip>"
            #  node_type: master
            #- name: wazuh-2
            #  ip: "<wazuh-manager-ip>"
            #  node_type: worker
            #- name: wazuh-3
            #  ip: "<wazuh-manager-ip>"
            #  node_type: worker

        # Wazuh dashboard nodes
        dashboard:
            - name: dashboard
            ip: "<dashboard-node-ip>"
    ```

3. Execute o assistente de instalação do Wazuh com a opção `--generate-config-filesde` gerar a chave de cluster, os certificados e as senhas do Wazuh necessários para a instalação. Você pode encontrar esses arquivos em `./wazuh-install-files.tar`.  

    ```bash
        bash wazuh-install.sh --generate-config-files
    ```

4. Copie o wazuh-install-files.tararquivo para todos os servidores da implantação distribuída, incluindo o servidor Wazuh, o indexador Wazuh e os nós do painel Wazuh. Isso pode ser feito usando o scputilitário.

#### Instalação do nó indexador Wazuh

Siga estas etapas para instalar e configurar um indexador Wazuh de nó único ou de vários nós.

1. Baixe o assistente de instalação do Wazuh. Pule esta etapa se você realizou a configuração inicial no mesmo servidor e o assistente de instalação do Wazuh já está no seu diretório de trabalho:

    ```bash
        curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
    ```

2. Execute o assistente de instalação do Wazuh com a opção `--wazuh-indexer` e o nome do nó para instalar e configurar o indexador Wazuh. O nome do nó deve ser o mesmo usado na `config.yml` configuração inicial, por exemplo, `node-1`.

    ```markdown
    *Observação* Certifique-se de que uma cópia do wazuh-install-files.tar,  
        criada durante a etapa de configuração inicial, seja colocada no seu  
        diretório de trabalho.
    ```  

    ```bash
        bash wazuh-install.sh --wazuh-indexer node-1
    ```

    Repita esta etapa do processo de instalação para cada nó indexador Wazuh no seu cluster. Em seguida, prossiga com a inicialização do seu cluster de nó único ou multinós na próxima etapa.  

#### Inicialização do cluster

O estágio final da instalação do cluster de nó único ou de vários nós do indexador Wazuh consiste em executar o script de administração de segurança.

1. Execute o assistente de instalação do Wazuh com a opção --start-clusterem qualquer nó do indexador Wazuh para carregar as novas informações de certificados e iniciar o cluster.

    ```bash
        bash wazuh-install.sh --start-cluster
    ```

    ```markdown
    *Observação* Você só precisa inicializar o cluster uma vez,  
    não há necessidade de executar este comando em cada nó.
    ```  

#### Testando a instalação do cluster

Verifique se o indexador Wazuh foi instalado corretamente e se o cluster do indexador Wazuh está funcionando conforme o esperado seguindo as etapas abaixo.  

1. Execute o seguinte comando para obter a senha do administrador :

    ```bash
        tar -axf wazuh-install-files.tar wazuh-install-files/wazuh-passwords.txt -O | grep -P "\'admin\'" -A 1
    ```

2. Execute o seguinte comando para confirmar que a instalação foi bem-sucedida. Substitua `<WAZUH_INDEXER_IP_ADDRESS>` pelo endereço IP do indexador Wazuh e use a senha obtida na saída do comando anterior:

    ```bash
        curl -k -u admin https://<WAZUH_INDEXER_IP_ADDRESS>:9200
    ```

    *Output*

    ```bash
        {
        "name" : "node-1",
        "cluster_name" : "wazuh-cluster",
        "cluster_uuid" : "095jEW-oRJSFKLz5wmo5PA",
        "version" : {
            "number" : "7.10.2",
            "build_type" : "rpm",
            "build_hash" : "db90a415ff2fd428b4f7b3f800a51dc229287cb4",
            "build_date" : "2023-06-03T06:24:25.112415503Z",
            "build_snapshot" : false,
            "lucene_version" : "9.6.0",
            "minimum_wire_compatibility_version" : "7.10.0",
            "minimum_index_compatibility_version" : "7.0.0"
        },
        "tagline" : "The OpenSearch Project: https://opensearch.org/"
        }
    ```

3. Execute o seguinte comando para verificar se o cluster está funcionando corretamente. Substitua `<WAZUH_INDEXER_IP_ADDRESS>` pelo endereço IP do indexador Wazuh e digite a senha do adminusuário do indexador Wazuh quando solicitado:

    ```bash
        curl -k -u admin https://<WAZUH_INDEXER_IP_ADDRESS>:9200/_cat/nodes?v
    ```

    A saída do comando deve ser semelhante à seguinte:

    *Output*  

    ```bash
        ip              heap.percent ram.percent cpu load_1m load_5m load_15m node.role node.roles                               cluster_manager name
    192.168.107.240           19          94      4    0.22    0.21    0.20    dimr      data,ingest,master,remote_cluster_client *               node-1
    ```

#### Desativar atualizações do Wazuh

Recomendamos desabilitar os repositórios de pacotes Wazuh após instalar todos os componentes neste servidor para evitar atualizações acidentais.

Execute o seguinte comando somente após concluir todas as instalações:

```bash
    sed -i "s/^deb /#deb /" /etc/apt/sources.list.d/wazuh.list
    apt update
```

#### Próximos passos

O indexador Wazuh foi instalado com sucesso e você pode prosseguir com a instalação do servidor Wazuh. Para executar esta ação, consulte a seção Instalando o servidor Wazuh usando o método de instalação assistida.

___
[< Guia de Instalação](Installation_guide.md)  
[Instalação Servidor Wazuh >](Install_server.md)  
