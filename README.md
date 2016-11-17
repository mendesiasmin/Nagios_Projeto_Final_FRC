# Fundamentos de Redes de Computadores - FGA2016
* Iasmin Santos Mendes, 14/0041940
* João Paulo Bushe da Cruz, 14/0023348

## Projeto Final: Nagios

### Problema
Garantir a estabilidade e correto funcionamento de uma rede de computadores, para que esta possa prover constantemente os serviços baseados em redes.

### Introdução
Na década de 80,  o avanço da tecnologia e o início da integração entre comunicação e computadores proporcionaram o desenvolvimento de um novo panorâma nos processos de comunicação e na prórpia organização das empresas. De forma que um computador de alto desempenho passou a ser substitído por um conjunto de computadores de mais baixo custo, interconectados entre si. Neste contexto, surgiram as redes de computadores e a necessidade de gerenciar e monitorar todos estes dispositivos conectados.

A comunicação em redes promoveu o encurtamento de distâncias e a base para o atual mundo globalizado em que vivemos hoje [BENINI e DAIBERT]. Levando a praticidade de acesso a serviços remotos, rapidez e eficácia das comunicações, e criando dependências entre serviços distintos. Para manter a viabilidade desses serviços  é necessário servidores ativos e redes funcinando corretamente. Dessa forma, o monitoramento da rede torna-se uma tarefa essencial para identificar problemas e prever possíveis falhas no sistema. Além de facilitar tomadas de decisões quanto ao planejamento, adequação e expansibilidade da rede.

O Nagios consiste em um software voltado a prover uma ferramenta prática que auxilie os administradores de rede no monitoramento e controle da mesma. Inicialmente, foi lançado com o nome Netsaint por Ethan Galstad para sistemas Linux, e somente depois foi desenvilvido para outros sistemas Unix. O programa conta com código aberto e licenciado pela GPL – General Public License.

### Nagios
#### Ferramenta para monitoramento de Redes

  De acordo com Kurose, um **dispositivo gerenciado** é um equipamento de rede, incluindo seu software, que reside em uma rede gerenciada, como um hospedeiro, um roteador, ou qualquer outro elemento conectado a esta rede. Cada dispositivo gerenciado é composto por elementos de hardware e parâmetros de configuração, os quais quando sob administração de uma ferramenta de monitoramento são denominados **objetos gerenciáveis**. Os dados e informações colhidos sobre estes objetos durante o monitoramento são armazenados em uma Base de Informações de Gerenciamento – MIB. Completando o quadro, cada dispositivo monitorado também possui um **Agente de gerenciamento** de rede, o qual é responsável por realizar a comunicação com a **entidade de gerenciamento**.

No caso particular do Nagios, este atua sobre um servidor, agindo como a respectiva entidade de gerenciamento, podendo monitorar hosts e serviços integrados a rede, os quais tenham instalados em seu sistema os pluguins que o auxiliam na coleta de dados. Estes plugins por sua vez, se identificam no papel de Agente de gerenciamento, ou seja, o processo sendo executado, por linha de comando, no dispositivo gerenciado para coletar as informações requisitadas pelo servidor central. Essa arquitetura modular baseada em plugins utilizada pela ferramenta torna o processo de monitoração organizado e escalonável. Permitindo que administradores de rede possam facilmente adptar o uso do Nagios as particularidades da rede, criando plugins específicos para os seus problemas e para diversas aplicações.

A checagem de serviços é realizada de maneira paralelizada, assim, não há possibilidade de um dispositivo não ser verificado por limitações de tempo. Também não há limites para o número de hosts a serem monitorados pela aplicação, a não ser pelo prório hardware do servidor em uso. 

O serviço de monitoração oferecido é definido em arquivos, abaixo encontra-se os principais arquivos de configuração e suas respectivas funcionalidades:

* nagios.cfg
* resource.cfg - Armazena as variáveis que facilitam o acesso às chamadas aos plugins, podendo as mesmas serem personalizadas.
* service.cfg - Identifica os serviços que serão monitorados e as métricas aplicadas a cada um dos dos clientes.
* host.cfg - Define os clientes que serão monitorados, podendo também agrupá-los de forma a organizar melhor a visão lógica da rede e simplificar as notificações.
* contact.cfg - Parâmetros em relação ao responsáveis pela rede que receberão as notificações.
* timeperiods.cfg - Delimita o periódo de tempo no qual é válido realizar a verificação da rede e enviar notificações sobre o estado da mesma.
* command.cfg - Configuração dos comandos usados para monitoramento dos hosts.
* CGI.cfg - Arquivo de configuração das permissões de usuários

Os registros dos dados coletados durante o monitoramento podem ser armazenados em um banco de dados ou em um arquivo de texto no formato de log. Esta última opção caracteriza-se por ser mais simples de implementar, contudo é mais lenta no acesso aos dados para gerar os relatórios e mais árduo a extração de dados personalizados. O banco de dados, por sua natureza, caracteriza-se por ser mais eficaz no tratamento de muitos dados.

A implementação de um software como tal facilita a resolução de problemas diversos como conectividade e integração de plataformas, além de permitir ao administrador da rede detectar falhas antes que os próprios usuários as percebam. Tornando mais eficiente o processo de gerenciamento e manutenção da rede.  O Nagios percorre a rede procurando possíveis warnings e estados críticos, podendo ser configurado para enviar mensagens via SMS, e-mail, pager ou outros meios para os administrados, ou mesmo para um grupo específico de responsáveis dependendo do problema encontrado.

#### Serviços

Os serviços ofertados por esta ferramenta ocorrem por meio de algortimos de verificação para avaliar o desempenho dos serviços prestados. O Nagios permite analisar tanto hosts quanto serviços  e realizar desde monitoramentos simples, como identificar se um dispositivo está conectado a rede por meio do PING, a monitoramentos mais complexos, como uso da CPU e outros hardwares em questão. Dentre os protocolos que podem ser moitorados pelo Nagios tem se como exemplos SMTP, POP3, HTTP, NNTP e ICMP. 

Um protocolo particular que merece ser mencionado, é o SNMP – Simple Network Management Protocol que atua como um agente de monitoração. Neste protocolo a entidade de monitoramento envia um OID – Object Identifier para o equipamento monitorado, visando obter diversas informações sobre o seu funcionamento, dentre elas estão:

* Uso de CPU;
* Uso de Memória;
* Configurações de rede;
* Atividade de rede (Download e upload);
* Usuários conectados;
* Serviços ativos.

Outras funcionalidades também oferecidas pela aplicação consistem na capacidade de definir a rede hierarquicamente, e de definir tratamentos de eventos para situações pré-determinadas ou para resoluções pró-ativas  de problemas. Além do mais, com base na toplogia da rede registrada pela aplicação, se ela identifica que um host só pode ser acessado por um determinado roteador da rede, e em algum momento este roteador cai, o Nagios reporta que o sistema está inatingível e para de gerar novos pedidos de verificação, para não sobrecarregar a rede.

O Nagios tabém coordena todas as tarefas de monitoração, a periodicidade de verificação, limita o tempo de execução de uma tarefa, seleciona os usuários que serão notificados e gera relatórios. Os relatórios são contém o intervalo de duração de cada problema, a porcentagem de tempo que o serviço esteve em funcionamento, histograma de um dispositivo gerenciável e filtragem de alertas por grupos os horas de serviços.

A aplicação dá também suporte a implementação de monitoramento distribuído ou redundante por meio do Nagios. O primeiro consiste em instalar vários servidores de monitoramento pela rede, os quais se comunicam com os agentes gerenciados acerca da coleta de dados, e enviam os mesmos para o servidor-mestre. Permite também monitoramento adaptativo, sendo possível alterar parâmetros de configuração sem ter que reinicializar a aplicação.

#### Instalação e Configuração

Recursos Utilizados:

* Nagios 4.2.2
* Nagios Plugins 2.1.2
* Ubuntu 14

Recursos Necessários para a instalação:

* Servidor instalado

sudo apt-get install build-essential libgd2-xpm-dev apache2-utils unzip

* Compilador GCC
* Bibliotecas GD

##### 1.Criar o usuário Nagios e senha

$ sudo useradd -m nagios

$ sudo passwd nagios

##### 2.Criar grupo Nagios

$ sudo groupadd nagcmd

$ sudo usermod -a -G nagcmd nagios

$ sudo usermod -a -G nagcmd www-data

