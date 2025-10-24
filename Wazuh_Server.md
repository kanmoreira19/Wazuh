# Conhecendo o Wazhu

## Componentes

### Servidor Wazuh

O servidor Wazuh é o componente central responsável pela análise dos dados coletados dos agentes Wazuh e dos dispositivos sem agente. Ele detecta ameaças, anomalias e violações de conformidade regulatória em tempo real, gerando alertas quando atividades suspeitas são identificadas. Além da detecção, o servidor Wazuh permite o gerenciamento centralizado, configurando remotamente os agentes Wazuh e monitorando continuamente seu status operacional.

O servidor Wazuh utiliza múltiplas fontes de inteligência de ameaças e enriquece alertas com dados contextuais para aumentar a precisão da detecção. Isso inclui o mapeamento de eventos para a estrutura MITRE ATT&CK, a detecção de vulnerabilidades com o serviço Wazuh CTI e o alinhamento das descobertas com padrões regulatórios como PCI DSS, GDPR, HIPAA, benchmarks CIS e NIST 800-53. Esses recursos fornecem às equipes de segurança insights práticos para busca de ameaças, detecção de vulnerabilidades e monitoramento de conformidade regulatória.

O servidor Wazuh integra-se a plataformas externas para oferecer suporte a fluxos de trabalho otimizados. Exemplos incluem sistemas de emissão de tickets como ServiceNow, Jira e PagerDuty, bem como ferramentas de comunicação como Slack. Essas integrações ajudam a automatizar o rastreamento de incidentes, acelerar os tempos de resposta e melhorar a colaboração entre as equipes de operações de segurança.

#### Componentes do servidor

O servidor Wazuh é composto por vários componentes listados abaixo que têm funções diferentes, como registrar novos agentes, validar a identidade de cada agente e criptografar as comunicações entre o agente Wazuh e o servidor Wazuh.

* **Serviço de inscrição de agentes:** Registra novos agentes Wazuh e gera e distribui chaves de autenticação exclusivas para cada agente. Funciona como um serviço de rede e suporta autenticação baseada em certificados TLS e SSL, ou inscrição usando uma senha fixa.

* **Serviço de conexão de agentes:** gerencia a comunicação entre os agentes Wazuh e o servidor Wazuh. Ele valida as identidades dos agentes Wazuh usando chaves de inscrição, aplica criptografia para transferência segura de dados e permite o gerenciamento centralizado de configurações para enviar remotamente as configurações atualizadas dos agentes.

* **Mecanismo de análise:** No centro dos recursos de detecção de ameaças do Wazuh, o mecanismo de análise processa os dados de segurança recebidos usando decodificadores e regras:

  * Os decodificadores classificam os tipos de log (por exemplo, eventos do Windows, logs SSH, logs do servidor web) e extraem campos relevantes, como endereços IP, nomes de usuários e IDs de eventos.

  * As regras comparam eventos decodificados com padrões conhecidos para detectar ameaças e anomalias. Quando acionadas, as regras geram alertas e invocam ações de resposta a incidentes, como bloqueio de endereços IP, encerramento de processos maliciosos ou remoção de artefatos de malware.

* API do servidor Wazuh: fornece uma interface programática para interagir com o servidor Wazuh. Ela permite que administradores que usam o painel do Wazuh ou a linha de comando realizem o seguinte, mas não se limita a:

  * Configurar e gerenciar agentes ou servidores

  * Monitore a integridade do sistema e o status da infraestrutura

  * Alertas de consulta e dados de endpoint

  * Criar ou atualizar decodificadores e regras

* **Daemon de cluster Wazuh:** permite escalonamento horizontal vinculando vários servidores Wazuh em um cluster. O uso de um balanceador de carga proporciona alta disponibilidade, tolerância a falhas e distribuição de carga.

* **Filebeat:** Encaminha eventos e alertas do mecanismo de análise Wazuh para o indexador Wazuh.

___
[< Componentes](Wazuh_Components.md)  
[Indexador Wazuh >](Wazuh_Indexer.md)
