**Assistente:** Como posso ajudá-lo?

---

**Usuário:** eu sou novo em sage, você pode me guiar para que eu aprenda a configurar?

---

**Assistente:** Olá! É ótimo que você esteja começando a utilizar o SAGE. Para te guiar na configuração, preciso entender melhor qual é o seu objetivo. Para começar, me fale:

- Qual é o tipo da sua base de dados? É uma base SCADA ou EMS?
- Qual o protocolo que você vai utilizar para a comunicação? Você vai se conectar a IEDs, UTRs, ou a outros centros de controle?
- Você tem alguma experiência com sistemas SCADA?

Com essas informações, posso te ajudar a entender os conceitos básicos e te indicar os passos para configurar o SAGE de acordo com as suas necessidades. 😉

---

**Usuário:** é uma base scada. vou precisar usar iec 61850, e não tenho nenhuma experiência com scada. antes de configurar eu queria que você me explicasse em termos gerais o sistema e o workflow. estou perdido!

---

**Assistente:** Calma! É normal se sentir perdido no começo. O SAGE pode parecer complexo, mas vamos por partes.

Em termos gerais, o SAGE é um sistema SCADA (Supervisory Control And Data Acquisition) utilizado para monitorar e controlar sistemas elétricos. Ele funciona como um "cérebro" que coleta dados de diversos equipamentos no campo, como IEDs (Intelligent Electronic Devices) e UTRs (Unidades Terminais Remotas), e os apresenta de forma organizada para o operador. O operador, por sua vez, pode visualizar esses dados, analisar o estado do sistema, e realizar ações de controle, como abrir ou fechar disjuntores, por exemplo.

Para te ajudar a visualizar o workflow, pense em três etapas principais:

- **Aquisição de dados:** O SAGE se comunica com os equipamentos no campo (IEDs e UTRs) através de protocolos específicos, como o IEC 61850, para receber informações sobre o estado do sistema elétrico. Essa comunicação pode ser realizada através de redes locais (LANs) ou de redes de longa distância (WANs).
- **Processamento e organização:** O SAGE recebe os dados brutos dos equipamentos e os converte para um formato que o operador possa entender, realizando a validação, a normalização, e a organização das informações. Ele também realiza cálculos, filtros, e outras operações para oferecer dados adicionais e indicadores relevantes.
- **Apresentação e controle:** O SAGE disponibiliza os dados processados para o operador através de interfaces gráficas, telas, relatórios, e outras ferramentas. O operador pode então analisar o estado do sistema, identificar eventuais problemas, e realizar ações de controle sobre os equipamentos, através do próprio SAGE.

Para te dar uma ideia mais prática:

- Imagine que você precisa monitorar o estado de um disjuntor em uma subestação.
- O disjuntor está conectado a um IED que, por sua vez, está conectado ao SAGE através de um protocolo IEC 61850.
- O SAGE recebe informações sobre o disjuntor, como se ele está aberto ou fechado, e a corrente que está passando por ele.
- O SAGE processa esses dados e os apresenta em uma tela, com informações como o estado do disjuntor, a corrente, e um indicador de alarme caso a corrente seja muito alta.
- O operador pode então analisar esses dados, e, se necessário, enviar um comando para o disjuntor através do SAGE, para abrir ou fechar ele.

Configurar o SAGE envolve definir todos esses aspectos:

- Quais equipamentos você quer monitorar?
- Como você vai se conectar a eles (protocolos e configurações de rede)?
- Como você quer organizar os dados?
- Quais cálculos você precisa realizar?
- Quais telas e relatórios você quer utilizar?

Entender a base de dados do SAGE é crucial para fazer todas essas definições. A base de dados contém a descrição de cada ponto, a sua localização, o seu tipo, o seu comportamento, e as regras de controle.

Agora que você tem uma ideia geral do SAGE e do workflow, vamos começar a explorar a configuração da base de dados. 😉

---

**Usuário:** a base de dados é em que formato? é um banco de dados tipo SQL Server ou MySQL?

---

**Assistente:** A base de dados do SAGE não é um banco de dados relacional como SQL Server ou MySQL. O SAGE utiliza um formato próprio de arquivos de texto, com extensão .dat.

Esses arquivos .dat são organizados em tabelas, e cada tabela representa uma entidade do sistema, como pontos, equipamentos, configurações, e outros elementos. Cada registro na tabela corresponde a uma instância da entidade, e os dados são armazenados em formato chave-valor.

Por exemplo, a tabela PAS.dat contém a descrição dos pontos analógicos lógicos do sistema. Cada registro na tabela PAS.dat representa um ponto analógico, com informações como:

```plaintext
ID: Identificador único do ponto.
NOME: Descrição do ponto.
LIA: Limite Inferior de Alarme.
LSA: Limite Superior de Alarme.
TIPO: Tipo da grandeza medida (MW, KV, etc).
```

A configuração da base de dados do SAGE é feita através da edição manual desses arquivos .dat. Você pode usar um editor de texto simples como o vim ou nano, ou um editor mais avançado como o gedit ou kate.

---

**Usuário:** o que significa exatamente um "ponto analógico lógico"? por que "lógico"?

---

**Assistente:** Você está com uma ótima pergunta! É importante entender a diferença entre pontos físicos e pontos lógicos no SAGE.

"Ponto analógico lógico" se refere a um valor analógico, ou seja, um valor que varia continuamente em uma escala, como a tensão, a corrente, a potência ativa, a potência reativa, a frequência, etc. O "lógico" se refere à representação do ponto no sistema SAGE, que é diferente da sua representação física no equipamento.

Vamos imaginar um exemplo prático:

1. **Ponto físico:**

    - Você tem um transformador na subestação que está medindo a corrente em um dos seus enrolamentos.
    - Essa medida da corrente está disponível no IED do transformador.
    - O IED representa essa medida com um endereço físico, como "1-1-1-1-1", e um valor numérico.
    - Esse é o ponto físico que o SAGE precisa "ler".

2. **Ponto lógico:**

    - Para o SAGE funcionar de forma mais intuitiva para o operador, ele precisa organizar esses pontos físicos em uma estrutura lógica.
    - Um "ponto analógico lógico" é a representação organizada do ponto físico dentro do SAGE, com um identificador único, uma descrição, um tipo, e informações adicionais que permitem ao operador entender o ponto.
    - No exemplo do transformador, o ponto lógico poderia ser chamado de "TR_LT12-CORRENTE_A", com a descrição "Corrente Fase A do Transformador da LT12", o tipo "AMP" (corrente), e o valor em unidade de engenharia (A - Ampères).

**Resumindo:**

- **Ponto físico:** É a representação da medida no equipamento, com endereço físico e valor numérico.
- **Ponto lógico:** É a representação organizada do ponto físico no SAGE, com identificador, descrição, tipo, e outras informações úteis para o operador.

A base de dados do SAGE contém a descrição de todos os pontos lógicos, incluindo os pontos analógicos lógicos. É através da base de dados que você define as características e as relações entre os pontos lógicos e os pontos físicos, criando uma estrutura organizada para o sistema. 😉

Espero ter esclarecido sua dúvida. Se precisar de mais detalhes, é só perguntar!