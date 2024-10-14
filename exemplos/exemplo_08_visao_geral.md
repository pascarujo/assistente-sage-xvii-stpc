**Assistente:** Como posso ajudá-lo?

---

**Usuário:** você pode me dar uma ideia geral de como funciona a configuração de uma base?

---

**Assistente:** Claro! A configuração de uma base no SAGE envolve definir as entidades, atributos e relacionamentos que representam os elementos do sistema elétrico que você deseja monitorar e controlar.

Aqui está um resumo geral do processo:

**Definição da Estrutura da Base:**

- Entidades: Representam os elementos do sistema elétrico (Ex: Subestação, Disjuntor, Linha de Transmissão, Transformador, Unidade Geradora).
- Atributos: Descrevem as características de cada entidade (Ex: Nome da subestação, Tensão nominal da linha, Potência nominal do transformador).
- Relacionamentos: Indicam como as entidades se conectam (Ex: Uma linha de transmissão está conectada a uma subestação).

**Configurar os Protocolos de Comunicação:**

- Conversores de Protocolo: Definir os protocolos utilizados para comunicar com os equipamentos do sistema (Ex: DNP3, IEC 61850, IEC 101).
- Transportadores de Protocolo: Especificar o tipo de transporte usado para enviar os dados (Ex: TCP/IP, Serial, Ethernet).

**Definir as Ligações SCADA (LSCs):**

- Aquisição: Configurar as conexões para receber dados dos equipamentos.
- Distribuição: Configurar as conexões para enviar comandos aos equipamentos ou dados para outros centros de controle.
- Mistas: Configurar conexões que combinam aquisição e distribuição.

**Criar os Terminais (TACs e TDDs):**

- TACs (Terminais de Aquisição e Controle): Agrupar os pontos lógicos de aquisição e controle, definindo os limites de alarme e o comportamento.
- TDDs (Terminais de Distribuição de Dados): Agrupar os pontos lógicos de distribuição.

**Definir os Pontos Lógicos:**

- Analógicos: Configurar os pontos que representam grandezas contínuas (Ex: Tensão, Corrente, Potência).
- Digitais: Configurar os pontos que representam estados binários (Ex: Estado de um disjuntor - aberto ou fechado).
- Totalizados: Configurar os pontos que representam contagens acumuladas (Ex: Energia).
- Controle: Configurar os pontos que permitem o controle dos equipamentos (Ex: Comandos para abrir/fechar disjuntores, setpoints).
- Informação: Configurar os pontos que representam dados textuais ou strings.

**Configurar o Controle de Acesso (Autorizações):**

- Áreas de Responsabilidade (AORs): Dividir o sistema em áreas lógicas, limitando o acesso dos operadores.
- Grupos de Ações (GRACTs): Agrupar as ações que os operadores podem realizar.
- Papéis: Atribuir papéis aos operadores, definindo as ações que podem ser executadas.

**Configurar a Apresentação Gráfica:**

- Paleta de Cores (COR): Definir as cores que serão usadas nas telas.
- Grupos de Componentes (GRUPO): Criar grupos de componentes para facilitar a organização das telas.
- Títulos e Textos (TXT): Definir os títulos e textos que serão usados nas telas.

**Atualizar a Base de Dados:**

- Usar o comando AtualizaBD fria fonte para gerar a base de dados a partir dos arquivos .dat.

**Observações:**

- O processo de configuração da base envolve diversos arquivos .dat que são organizados em diretórios específicos.
- A utilização de ferramentas como o xml61850 pode auxiliar na importação de configurações a partir de arquivos XML.
- É importante consultar a documentação do SAGE para obter informações detalhadas sobre a configuração de cada entidade, atributo e relacionamento.

Espero que essas informações sejam úteis para você entender a configuração de uma base no SAGE. Se tiver mais alguma dúvida, não hesite em perguntar. 😉


---