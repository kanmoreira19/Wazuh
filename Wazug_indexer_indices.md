# Conhecendo o Wazhu

## Índices do Indexador Wazuh

Um índice é uma coleção de documentos relacionados entre si. O indexador Wazuh usa índices para armazenar e organizar dados de segurança para recuperação rápida. O Wazuh usa os seguintes padrões de índice para armazenar esses dados:

* wazuh‑alerts-* : Este é o padrão de índice para alertas gerados pelo servidor Wazuh.  

* wazuh‑archives-* : Este é o padrão de índice para todos os eventos enviados ao servidor Wazuh.  

* wazuh‑monitoring-* : Este é o padrão de índice para o status dos agentes Wazuh.  

* wazuh‑statistics-* : Este é o padrão de índice que mostra as métricas de desempenho do servidor Wazuh. Ele contém informações que mostram quantos eventos são recebidos, processados ​​e descartados pelo servidor Wazuh.  

* wazuh-states-vulnerabilities-* : Este é o padrão de índice para informações sobre vulnerabilidades detectadas nos endpoints que estão sendo monitorados.  

* wazuh-states-inventory-hardware-* : Este é o padrão de índice para informações básicas sobre componentes de hardware em um endpoint monitorado.  

* wazuh-states-inventory-hotfixes-* : Este é o padrão de índice para atualizações instaladas em um endpoint Windows. O módulo de detecção de vulnerabilidades Wazuh usa isso para descobrir quais vulnerabilidades foram corrigidas em um endpoint Windows.  

* wazuh-states-inventory-interfaces-* : Este é o padrão de índice paraupedowninformações de transferência de pacotes sobre interfaces de rede em um ponto de extremidade monitorado.  

* wazuh-states-inventory-networks-* : Este é o padrão de índice para endereços IPv4 e IPv6 associados a cada interface de rede em um ponto de extremidade monitorado.  

* wazuh-states-inventory-packages-* : Este é o padrão de índice para pacotes de software atualmente instalados em um endpoint.  

* wazuh-states-inventory-ports-* : Este é o padrão de índice para portas de rede abertas em um ponto de extremidade monitorado.  

* wazuh-states-inventory-processes-* : Este é o padrão de índice para processos do sistema em execução em um endpoint monitorado.  

* wazuh-states-inventory-protocols-* : Este é o padrão de índice para detalhes de configuração de roteamento de rede e protocolos para cada interface de rede em um ponto de extremidade monitorado.  

* wazuh-states-inventory-system-* : Este é o padrão de índice para informações sobre o sistema operacional, nome do host e arquitetura em um endpoint monitorado.  

Para personalizar ainda mais o padrão de índice para alertas, você pode criar um padrão de índice personalizado.
