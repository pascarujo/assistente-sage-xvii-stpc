**Usuário:** quais as principais tabelas do sage?

---

**Assistente:** As principais tabelas do SAGE, no contexto SCADA, estão relacionadas aos subsistemas de Suporte Computacional (SSC) e Comunicação e Pré-processamento de Dados (SCD). Abaixo, uma lista das tabelas mais relevantes, agrupadas por função e com uma breve descrição:

**SSC - Rede de Difusão Confiável:**

- PRO: Define os processos do SAGE, como aquisição, controle, histórico, etc.
- CTX: Define o contexto do SAGE, geralmente "TR" para Tempo Real.
- INP: Define as instâncias dos processos em cada nó da rede.
- NOH: Define os nós da rede de difusão confiável.
NOCT: Relaciona nós com contextos.
- PRCT: Relaciona processos com contextos.
- SEV: Define as severidades dos alarmes, como Normal, Advertência, Urgência, etc.

**SSC - Serviço de Alarmes e Eventos:**

- MAP: Define os macro alarmes, agrupando alarmes/eventos por critérios específicos.
- E2M: Relaciona pontos lógicos, totalizados, digitais e ocorrências com macro alarmes.
- GRPOCR: Define grupos de ocorrências de alarmes.
- OCR: Define as ocorrências de alarmes e eventos.
- TELA: Define as telas associadas a ocorrências ou instalações.
- CFSIS: Define parâmetros genéricos do sistema, como perfis de debug, modelos PI-AF, etc.

**SCD - Serviço de Comunicação de Dados:**

- TCV: Define os tipos de conversores de protocolo, como DNP3, IEC 61850, etc.
- TTP: Define os tipos de transportadores de protocolo, como TCP/IP, X25, etc.
- GSD: Define os gateways do sistema, que gerenciam as ligações com UTRs e centros de controle.
- CXU: Define as conexões com UTRs, incluindo parâmetros de aquisição, failover, etc.
- ENU: Define os enlaces de conexão com UTRs.
- UTR: Define as UTRs físicas e virtuais, incluindo endereço, timeout, etc.
- MUL: Define as multiligações com centros de controle, incluindo parâmetros de comunicação.
- ENM: Define os enlaces de multiligação.
- CNM: Define os canais lógicos em uma multiligação, com prioridade e configurações específicas.

**SCD - Serviço de Aquisição e Controle:**

- LSC: Define as ligações SCADA, com tipos (aquisição, distribuição, mista), conversores, transportadores e outros parâmetros.
- INS: Define as instalações, como usinas ou subestações.
- TAC: Define os Terminais de Aquisição e Controle, agrupando pontos lógicos para controle e monitoramento.
- CGS: Define os pontos de controle lógicos, com limites, tipos de controle, etc.
- TCTL: Define os tipos de controle, como abrir/fechar, habilitação/desabilitação, etc.
- PAS: Define os pontos analógicos lógicos, com limites de alarme, escalas, tipo de grandeza, etc.
- PTS: Define os pontos totalizados lógicos, com limites, tipo de grandeza, etc.
- PDS: Define os pontos digitais lógicos, com estados, tipo de grandeza, etc.
- RCA: Define as parcelas de cálculos estáticos compilados e interpretados.
- TCL: Define os tipos de cálculos, incluindo fórmulas e parâmetros.
- SITE: Define os sites, geralmente com informações do servidor de base de dados.
- COS: Define os centros de controle.
- SUBSIS: Define os subsistemas computacionais, como NAD e RTN.

**SCD - Patamar de Carga:**

- PTC: Define os patamares de carga para atualização automática de limites de pontos analógicos.
- TEMPO: Define os horários para atualização automática de limites.
- TGL: Define os tipos de grandezas e equipamentos para atualização automática de limites.
- FRD: Define os feriados fixos.
- DTS: Define os dias típicos da semana (dias úteis, fim de semana, etc.).

**SCD - Pontos Físicos:**

- CNF: Define as configurações físicas, agrupando pontos físicos de aquisição ou distribuição.
- NV1: Define os níveis 1 das configurações físicas, geralmente correspondentes a dispositivos do IED.
- NV2: Define os níveis 2 das configurações físicas, geralmente correspondentes a dados específicos do IED.
TN1: Define os tipos de entidades de nível 1.
- TN2: Define os tipos de entidades de nível 2.
- CGF: Define os pontos de controle físicos.
- PAF: Define os pontos analógicos físicos.
- PDF: Define os pontos digitais físicos.
- PIF: Define os pontos de informação físicos.
- PTF: Define os pontos totalizados físicos.
- RFI: Define os relacionamentos de filtros simples.
- RFC: Define os relacionamentos de filtros compostos.

**SCD - OPC UA:**

- NODE_OPC: Define os nodes do modelo OPC UA exportado pelo SAGE.
- REFNH_OPC: Define as referências não hierárquicas do modelo OPC UA.
- VAR_OPC: Define as variáveis do namespace zero do modelo OPC UA.

**IHM - Modelo de Apresentação:**

- COR: Define a paleta de cores do SAGE.
- GRCMP: Define os componentes de grupos de pontos para diálogos automáticos.
- GRUPO: Define os grupos de componentes para diálogos automáticos.
- REGRA: Define as regras para o registrador condicional.
- QLD: Define os indicadores de qualidade, com cores e símbolos.

**Controle de Geração:**

- CAG: Define os parâmetros do CAG (Controle Automático de Geração).
- BND: Define as bandas de rejeição do CAG.
- CEA: Define os parâmetros do controle adaptativo do CAG.
- ECA: Define os parâmetros do erro de controle de área do CAG.
- FLG: Define os flags de controle do CAG.
- FXG: Define as faixas de geração das unidades geradoras para o CAG.
MRPG: Define os motivos de reprogramação de geração.
- TCG: Define os temporizadores do CAG.
- UGE: Define as unidades geradoras, com parâmetros de operação, regulação, etc.

**Outras:**

- EST: Define as estações, geralmente com informações de localização e patamar de carga.
- EQP: Define os equipamentos, com tipo, localização, etc.
- CAR: Define as cargas, com dados de potência ativa e reativa.
- LTR: Define as linhas de transmissão, com dados de potência, impedância, etc.
- RAM: Define os ramais, com dados de potência, impedância, etc.
- TR2: Define os transformadores de 2 enrolamentos, com dados de potência, tap, etc.
- TR3: Define os transformadores de 3 enrolamentos, com dados de potência, tap, etc.
- ACO: Define as áreas de controle.
- ARE: Define as áreas elétricas.
- CIA: Define as companhias.
- CPB: Define as curvas de capabilidade.
- ECON: Define as estações controladas.
- GUGE: Define os grupos de geradores.
- TPREDE: Define os tipos de rede.
- UDE: Define as unidades de despacho.
- USI: Define as usinas.
- UFE: Define as unidades federativas.
- PMU: Define as unidades de medida fasorial (PMUs).

**Observações:**

Esta lista não é exaustiva, mas contém as tabelas mais importantes para a configuração SCADA do SAGE.
O SAGE também possui tabelas para funções EMS (Gerenciamento de Energia), que não foram descritas aqui.
Para detalhes específicos sobre cada tabela, consulte a documentação do SAGE.

É essencial que o usuário tenha conhecimento profundo do modelo de dados do SAGE para realizar a configuração de forma correta e eficiente.
