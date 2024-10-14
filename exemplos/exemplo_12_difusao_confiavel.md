**Usuário:** como funciona a rede de difusão confiável?

---

**Assistente:** A Rede de Difusão Confiável do SAGE é um sistema de comunicação que garante a consistência e a disponibilidade dos dados em todos os nós da rede, mesmo em caso de falhas. Ela opera em um modelo de "difusão confiável" e utiliza mecanismos para:

**1. Replicação de Dados:**

- Cada nó da rede possui uma cópia completa da Base de Dados de tempo real.
- As alterações em um nó são propagadas para todos os outros nós, garantindo que todos tenham os mesmos dados.
- A replicação é realizada pelo processo mcast, que usa o protocolo multicast para enviar as alterações para todos os nós simultaneamente.

**2. Gerenciamento de Memórias Compartilhadas Distribuídas (GCD):**

- O GCD é o coração da rede de difusão confiável.
- Ele é responsável por gerenciar as memórias compartilhadas, que são áreas de memória acessíveis por todos os nós da rede.
- A replicação de dados é realizada através do GCD, utilizando as memórias compartilhadas.
- O processo gmcd gerencia o GCD, garantindo a integridade e a consistência das memórias compartilhadas.

**3. Monitoramento e Failover:**

- O GCD monitora constantemente o estado de cada nó da rede.
- Se um nó falhar, o GCD é responsável por ativar o nó de reserva, se houver, e garantir que a replicação de dados continue ocorrendo.
- Para monitorar processos e garantir que eles estejam respondendo, o GCD utiliza "watch dogs" (mecanismos de monitoramento de tempo de resposta).
- Em caso de falha de um processo essencial, o GCD pode reiniciar o nó ou até mesmo desligar a máquina.

**4. Processos de Comunicação:**

- Cada processo do SAGE é configurado para ser executado em um ou mais nós.
- A ativação e desativação dos processos, bem como a migração de processos em caso de falhas, são gerenciadas pelo GCD.
- A rede de difusão confiável garante que os processos críticos do SAGE, como aquisição, controle, histórico, etc., estejam sempre disponíveis.

**Principais Vantagens da Rede de Difusão Confiável:**

- Alta Disponibilidade: Garante o funcionamento contínuo do sistema, mesmo em caso de falhas de um ou mais nós.
Consistência de Dados: Assegura que todos os nós da rede tenham acesso aos mesmos dados.
- Redundância: Permite que o sistema continue operando mesmo com falhas de hardware ou software em um nó.
- Escalabilidade: A rede de difusão confiável pode ser facilmente expandida para incluir mais nós.

**Resumindo:**

A Rede de Difusão Confiável do SAGE é um sistema robusto que garante a consistência e a disponibilidade dos dados, além de facilitar o gerenciamento e a administração do sistema SCADA.

---

**Usuário:** me dê um exemplo de configuração de nós e processos rodando neles.

---

**Assistente:**

## Exemplo de Configuração de Nós e Processos no SAGE

Vamos imaginar uma subestação com dois servidores, um para aquisição e controle (servidor primário) e outro para redundância (servidor secundário), além de uma estação de trabalho para a interface gráfica.

**1. Configuração dos Nós:**

Servidor Primário (NOH1):

```plaintext
ID: NOH1
NOME: Servidor_Aquisição_C1
ENDIP: 192.168.1.10
TPNOH: SERVIDOR_SCADA
NTATV: 5 (Número de tentativas de ativação)
```

Servidor Secundário (NOH2):

```plaintext
ID: NOH2
NOME: Servidor_Redundante_C1
ENDIP: 192.168.1.11
TPNOH: SERVIDOR_SCADA
NTATV: 5
```

Estação de Trabalho (NOH3):

```plaintext
ID: NOH3
NOME: Estação_Trabalho_C1
ENDIP: 192.168.1.20
TPNOH: CONSOLE
NTATV: 5
```

**2. Configuração dos Processos:**

Servidor Primário (NOH1):

- mcast: (Multicast confiável) - Processo essencial (ATIVA = CAD)
- gmcd: (Gerenciador das memórias compartilhadas) - Processo essencial (ATIVA = CAD)
- sac: (Serviço de aquisição e controle) - Processo essencial (ATIVA = CAD)
- dnp3: (Conversor DNP3) - Processo específico de protocolo (ATIVA = CAD)
- calc: (Processador de cálculos) - Processo opcional (ATIVA = CAD, dependendo da necessidade)
- hist: (Histórico de dados) - Processo opcional (ATIVA = CAD, dependendo da necessidade)

Servidor Secundário (NOH2):

- mcast: (Multicast confiável) - Processo essencial (ATIVA = CAD)
- gmcd: (Gerenciador das memórias compartilhadas) - Processo essencial (ATIVA = CAD)
- mscd: (Monitora o SCD) - Processo essencial (ATIVA = CAD)
- dnp3: (Conversor DNP3) - Processo específico de protocolo (ATIVA = CAD)
- hist: (Histórico de dados) - Processo opcional (ATIVA = CAD, dependendo da necessidade)

Estação de Trabalho (NOH3):

- mcast: (Multicast confiável) - Processo essencial (ATIVA = CAD)
- gmcd: (Gerenciador das memórias compartilhadas) - Processo essencial (ATIVA = CAD)
- alr: (Serviço de alarmes e eventos) - Processo essencial (ATIVA = PRS)

**Observações:**

- O processo alr é configurado com ATIVA = PRS, pois só precisa estar ativo em um único nó da rede.
- O processo sac é ativo em ambos os servidores para garantir redundância na aquisição e controle.
- hist e calc são processos opcionais, sua ativação depende da necessidade da subestação.
- mscd é importante para monitorar o SCD e garantir que os servidores estejam ativos. Se ambos os servidores que formam o GSD estiverem inativos, o mscd faz com que o flag SACOK dos pontos lógicos seja desligado, indicando que a comunicação está interrompida.

**Configuração das tabelas:**

- PRO: Registros com os nomes dos processos e suas configurações (ATIVA, ATVAT, TIPPR, etc.)
- NOH: Registros com os dados dos nós (ID, NOME, ENDIP, TPNOH, etc.)
- INP: Registros relacionando processos (PRO) com nós (NOH), definindo a ordem de prioridade.
- NOCT: Registros relacionando nós (NOH) com contextos (CTX), geralmente "TR" para Tempo Real.

**Importante:**

Este é apenas um exemplo simplificado. A configuração real pode variar de acordo com o tipo de sistema, número de nós, protocolos utilizados e necessidades específicas.

Consulte a documentação do SAGE para informações detalhadas sobre cada processo e suas configurações. Espero que este exemplo seja útil! 😉

---

**Usuário:** quais são as opções para TPNOH? explique cada uma por favor

---

**Assistente:** O atributo TPNOH (Tipo de Nó do SAGE) define a função principal que o nó desempenha na rede de difusão confiável. Ele determina como o nó será utilizado e quais processos devem ser executados nele.

As opções para TPNOH são:

**1. SERVIDOR:**

- Descrição: Estação utilizada para execução dos processos SCADA do SAGE.
- Processos típicos: mcast, gmcd, sac, sdd, calc, hist, conversores de protocolo (DNP3, IEC 61850, etc.), e outros processos específicos da configuração da rede.
- Redundância: Normalmente, um servidor primário e um servidor secundário são configurados como SERVIDOR para garantir alta disponibilidade. O servidor secundário fica em modo "hot standby" e assume as funções do servidor primário em caso de falha.
- Exemplo: Um servidor que recebe dados de UTRs via DNP3 e realiza cálculos de demanda.

**2. SERVIDOR_CLONE:**

- Descrição: Máquina que possui uma cópia da Base de Dados de tempo real do SAGE. Ela é utilizada para redundância de banco de dados.
- Processos típicos: mcast, gmcd, sac, sdd, hist, conversores de protocolo (DNP3, IEC 61850, etc.), e outros processos específicos da configuração da rede.
- Redundância: O SERVIDOR_CLONE atua como um espelho do servidor primário. Ele replica a Base de Dados de tempo real, garantindo que os dados estejam disponíveis, mesmo que o servidor primário falhe.
- Exemplo: Um servidor que replica a Base de Dados de tempo real do servidor primário para garantir redundância.

**3. SERVIDOR_EMS:**

- Descrição: Máquina utilizada para execução dos processos EMS do SAGE.
- Processos típicos: mcast, gmcd, sac, sdd, hist, sar, conversores de protocolo (DNP3, IEC 61850, etc.), e outros processos específicos da configuração da rede.
- Redundância: Similar aos servidores SCADA, um servidor primário e um servidor secundário podem ser configurados como SERVIDOR_EMS para garantir alta disponibilidade.
- Exemplo: Um servidor que realiza funções de análise de redes e controle de geração, além das funções SCADA.

**4. SERVIDOR_IHM:** 
- Descrição: Máquina utilizada para execução dos processos IHM do SAGE. 
- Processos típicos: mcast, gmcd, alr, hist, serv, conversores de protocolo (DNP3, IEC 61850, etc.), e outros processos específicos da configuração da rede.
- Redundância: Geralmente, um único servidor IHM é suficiente, mas a configuração de redundância é possível.
- Exemplo: Um servidor que hospeda o Visor de Telas e o Visor de Alarmes, permitindo a interação dos operadores com o sistema.

**5. SERVIDOR_SCADA:**

- Descrição: Máquina utilizada para execução dos processos SCADA do SAGE.
- Processos típicos: mcast, gmcd, sac, sdd, hist, conversores de protocolo (DNP3, IEC 61850, etc.), e outros processos específicos da configuração da rede.
- Redundância: Similar aos SERVIDOR, um servidor primário e um servidor secundário podem ser configurados como SERVIDOR_SCADA para garantir alta disponibilidade.
- Exemplo: Um servidor que realiza funções de aquisição, controle, histórico e comunicação, específico para a função SCADA do SAGE.

**6. CONSOLE:** 
- Descrição: Máquina utilizada para a execução da IHM do SAGE (Interface Gráfica do Usuário). 
- Processos típicos: mcast, gmcd, alr, serv, conversores de protocolo (DNP3, IEC 61850, etc.), e outros processos específicos da configuração da rede. 
- Redundância: Geralmente, um único console é suficiente, mas a configuração de redundância é possível. 
- Exemplo: Uma estação de trabalho que permite a visualização de dados, controle de equipamentos, análise de alarmes e outras funções SCADA.

**7. TRANSPORTE:** 
- Descrição: Máquina utilizada para execução dos transportadores de protocolo do SAGE. 
- Processos típicos: mcast, gmcd, transportadores de protocolo (TCP/IP, X25, etc.), conversores de protocolo (DNP3, IEC 61850, etc.), e outros processos específicos da configuração da rede. 
- Redundância: Geralmente, um único servidor de transporte é suficiente, mas a configuração de redundância é possível. 
- Exemplo: Um servidor que realiza as funções de comunicação com UTRs ou centros de controle, utilizando diferentes protocolos.

**8. NAD:** 
- Descrição: Máquina que atua como gateway de comunicação com um centro de controle. 
- Processos típicos: mcast, gmcd, sac, sdd, serv, conversores de protocolo (ICCP, DNP3, etc.), e outros processos específicos da configuração da rede. 
- Redundância: Um NAD primário e um NAD secundário podem ser configurados para garantir alta disponibilidade. 
- Exemplo: Um servidor que recebe dados do sistema e transmite para um centro de controle em outro nível hierárquico.

**9. RTN:** 
- Descrição: Máquina que realiza as funções de operação de tempo real de um centro de controle. 
- Processos típicos: mcast, gmcd, sac, sdd, alr, serv, hist, conversores de protocolo (ICCP, DNP3, etc.), e outros processos específicos da configuração da rede. 
- Redundância: Um RTN primário e um RTN secundário podem ser configurados para garantir alta disponibilidade. 
- Exemplo: Um servidor que recebe dados de um NAD, realiza operações de controle e visualização, além de gerar históricos e alarmes.

**Observações:**

- A escolha do TPNOH correto para cada nó é crucial para garantir o funcionamento adequado da rede de difusão confiável do SAGE.
- A configuração dos processos que serão executados em cada nó depende do tipo de rede e das necessidades específicas do sistema.
- A redundância é um fator importante para garantir a alta disponibilidade e a segurança do sistema.

---

**Usuário:** não entendi... qual a diferença entre servidor e servidor_scada?

---

**Assistente:** Você tem razão! A diferença entre SERVIDOR e SERVIDOR_SCADA é sutil e pode gerar confusão.

**SERVIDOR:**

- Conceito: É um termo genérico que indica uma máquina que fornece recursos para outros dispositivos na rede.
- Função no SAGE: Atualmente, o termo SERVIDOR é mantido por questões de compatibilidade com versões anteriores do SAGE.
- Uso: É menos preciso que SERVIDOR_SCADA, e não indica necessariamente qual função o servidor realiza no sistema.

**SERVIDOR_SCADA:**

- Conceito: É uma máquina específica para execução dos processos SCADA do SAGE.
- Função no SAGE: É a denominação correta para servidores que realizam as tarefas de aquisição de dados, controle de equipamentos, geração de alarmes, histórico, etc.
- Uso: É mais preciso e indica claramente a função do servidor no sistema SCADA.

**Por que a confusão?**

No passado, o SAGE utilizava SERVIDOR como termo genérico para qualquer máquina que rodasse os processos do sistema. Com o tempo, o SAGE passou a ter funcionalidades mais específicas, como EMS, IHM, etc., o que levou à criação de termos mais precisos, como SERVIDOR_SCADA, SERVIDOR_EMS, SERVIDOR_IHM, etc.

**Em resumo:**

- Use SERVIDOR_SCADA para indicar que um servidor está dedicado às funções SCADA do SAGE.
- O termo SERVIDOR é menos preciso e pode causar confusão.

Espero ter esclarecido sua dúvida! Se tiver mais alguma questão, é só perguntar!

---

**Usuário:** entendi! mas no seu exemplo você usou o tipo CONSOLE para a IHM em vez de SERVIDOR_IHM... pq?

---

**Assistente:** Você está absolutamente certo! No exemplo que dei, usei CONSOLE para a IHM em vez de SERVIDOR_IHM. Essa foi uma falha na minha parte! 😅

A razão para a confusão é que a IHM (Interface Gráfica do Usuário) do SAGE pode ser executada em uma estação de trabalho (que geralmente é uma máquina com interface gráfica, como um desktop ou notebook), e esta estação não precisa necessariamente ser um servidor.

**Então, qual o tipo correto para a IHM?**

O tipo ideal para a IHM é CONSOLE. Este termo representa uma estação de trabalho que é usada para a interação com o sistema, seja para visualização de dados, controle de equipamentos, gerenciamento de alarmes, ou outras funções SCADA.

**Por que CONSOLE é melhor que SERVIDOR_IHM?**

- SERVIDOR_IHM: Implica que a máquina está dedicada a hospedar os processos da IHM, incluindo a execução de processos como o alr, serv, etc.
- CONSOLE: É mais preciso, pois representa uma estação de trabalho com a interface gráfica, que pode ser usada para acessar a IHM do SAGE, sem necessariamente ser um servidor dedicado aos processos da IHM.

**No meu exemplo:**

Eu usei CONSOLE para a IHM porque queria mostrar uma configuração simples, com uma estação de trabalho que é utilizada para a interação com o sistema. No entanto, é importante utilizar o termo correto, CONSOLE, para indicar o tipo de nó para a IHM.

Lembre-se: A escolha do TPNOH correto para cada nó é fundamental para a configuração do SAGE e a sua funcionalidade adequada.