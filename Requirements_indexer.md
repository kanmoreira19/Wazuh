[Índice](Indice.md)  
___
## Guia de Instalação

### Instalação do Indexador Wazuh

O indexador Wazuh é um mecanismo de busca e análise de texto completo altamente escalável. Ele indexa e armazena alertas gerados pelo servidor Wazuh e oferece recursos de busca e análise de dados quase em tempo real. Se quiser saber mais sobre os componentes do Wazuh, consulte a seção ["Introdução"](README.md) .

Você pode instalar o indexador Wazuh em um único host ou distribuí-lo entre vários nós em uma configuração de cluster. A configuração de cluster oferece escalabilidade, alta disponibilidade e desempenho aprimorado.

Verifique os requisitos abaixo para começar a instalar o indexador Wazuh.

#### Requisitos

Verifique os sistemas operacionais suportados e os requisitos de hardware recomendados para a instalação do indexador Wazuh. Certifique-se de que o ambiente do seu sistema atenda a todos os requisitos e que você tenha privilégios de usuário root.

###### Sistemas operacionais recomendados
O indexador Wazuh requer um processador Intel, AMD ou ARM Linux de 64 bits (arquitetura x86_64/AMD64 ou AARCH64/ARM64) para ser executado. O Wazuh suporta as seguintes versões de sistema operacional:

* Amazon Linux 2, Amazon Linux 2023

* CentOS Stream 10

* Red Hat Enterprise Linux 7, 8, 9, 10

* Ubuntu 16.04, 18.04, 20.04, 22.04, 24.04

###### Recomendações de hardware

Você pode instalar o indexador Wazuh como um cluster de nó único ou de vários nós.

* Recomendações de hardware para cada nó

**Mínimo**  

| Componente | RAM (GB) | CPU (núcleos) |  
| - | :-: | :-: |  
|Indexador Wazuh| 4 | 2 |  

**Recomendado**  

| Componente | RAM (GB) | CPU (núcleos) |  
| - | :-: | :-: |  
|Indexador Wazuh| 16 | 8 |  

* Requisitos de espaço em disco: A quantidade de espaço em disco necessária depende dos alertas gerados por segundo (APS). Esta tabela detalha o espaço em disco estimado necessário por agente para armazenar 90 dias de alertas em um servidor indexador Wazuh, dependendo do tipo de endpoint monitorado.

| Endpoints Monitorados | APS | Armazenamento do Indexador (GB/90 dias) |
| - | :-: | :-: |
| Servidores | 0,25 | 3,7 |
| Estações | 0,1 | 1,5 |
| Dispositivos de Rede | 0,5 | 7,4 |

Por exemplo, para um ambiente com 80 estações de trabalho, 10 servidores e 10 dispositivos de rede, o armazenamento necessário no servidor indexador Wazuh para 90 dias de alertas é de 230 GB.

___
[< Instalação Rápida](Instalacao_rapida.md)  
[Instalação Indexador >](Install_Indexer.md)