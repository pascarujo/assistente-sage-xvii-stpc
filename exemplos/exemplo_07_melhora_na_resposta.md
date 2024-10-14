**Assistente:** Como posso ajudá-lo?

---

**Usuário:** Como a tabela CXU se relaciona com o modelo de dados do protocolo DNP3?

---

**Assistente:** A tabela CXU no SAGE, que representa a Conexão com Equipamentos de Aquisição e Controle (UTRs/CLPs), tem uma relação direta com o modelo de dados do protocolo DNP3. Vamos analisar como essa relação se manifesta:

**1. Camadas de Comunicação:**

O DNP3 trabalha com as camadas de aplicação, enlace e física. A CXU se relaciona principalmente com as camadas de enlace e física, definindo parâmetros que influenciam diretamente a comunicação entre o SAGE e as UTRs.

**2. Parâmetros da CXU e DNP3:**

- `AQANL`: Define o tempo em centésimos de segundo para aquisição periódica de dados analógicos (OBJ30), caso a CXU esteja relacionada a uma CNF configurada para DNP Level 0. Essa informação é crucial para determinar a frequência de varredura de dados analógicos no DNP3.
- `AQPOL`: Tempo em centésimos de segundo para verificação periódica do estado da UTR (OBJ50). Esse parâmetro influencia a frequência de polling words no DNP3, garantindo a manutenção da conexão com a UTR.
- `AQTOT`: Tempo em centésimos de segundo para integridade periódica de totalizadores (OBJ20). A CXU configura o intervalo de tempo para atualização de totalizadores no DNP3, garantindo a atualização do valor acumulado.
- `INTGR`: Tempo em centésimos de segundo para a leitura periódica de classe zero, caso a CXU esteja relacionada com uma Ligação de Aquisição. Isso define a frequência de coleta de eventos para transmissão em classes 1, 2 ou 3 no DNP3.
- `FAILP` e `FAILR`: Tempo em que o enlace principal e o enlace reserva permanecem primários antes do failover programado. Esses parâmetros influenciam a lógica de failover no DNP3, definindo quando o sistema deve alternar entre os enlaces.
- `NFAIL` e `SFAIL`: Definem o número máximo de tentativas de failover e o tempo máximo para aguardar o sincronismo das máquinas de estado dos dois enlaces. Esses parâmetros influenciam a estratégia de failover no DNP3, definindo quantas tentativas o sistema deve fazer para restabelecer a comunicação em caso de falha.

Em resumo, a tabela CXU no SAGE é uma ferramenta crucial para configurar os parâmetros da camada física e enlace do DNP3, garantindo o bom funcionamento da comunicação com as UTRs. A CXU, em conjunto com a CNF, define as características da comunicação com as UTRs, incluindo tempo de aquisição, polling, integridade, failover e outros parâmetros específicos do protocolo DNP3. Se tiver mais alguma dúvida sobre a configuração do SAGE com DNP3, me avise! 😄