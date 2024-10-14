**Usuário:** eu coloquei o seguinte ponto de controle na base e não consegui fazer ela rodar:

```plaintext
CGF
CNF=
CGS=	S1_ATR1_818
ID=	S1_C104_2_CDUP_400
NV2=	S1_C104_2_CDUP
KCONV=	DC_CF
ORDEM=	400

CGS
ID=	S1_ATR1-818
LMI1C=	 0
LMI2C=	 0
LMS1C=	 0
LMS2C=	 0
NOME=	ABRIR / FECHAR DISJUNTOR 818
PAC=	S1_ATR1_818
PINT=	
RSULT=  SIM
TAC=	S1_TAC
TIPO=	PDS
TIPOE=	CTCL
TPCTL=	CSAC
TRRAC=  20
AOR=	CURSO
```

---

**Assistente:** Entendi! Você está enfrentando problemas para ativar a base após adicionar este ponto de controle. Observando a configuração, me parece que há uma inconsistência entre o `ID` do `CGS` no `CGF` e o `ID` do `CGS`.

No `CGF`, você definiu `CGS=	S1_ATR1_818`, mas o `CGS` que você listou logo abaixo possui `ID=	S1_ATR1-818`. Perceba que no `ID` do `CGS` há um hífen ("-") onde deveria haver um underscore ("_"). 

Para corrigir isso, ajuste o `ID` do `CGS` para `S1_ATR1_818`, de forma que fique idêntico ao `CGS` referenciado no `CGF`:

```
CGS
ID=	S1_ATR1_818
LMI1C=	 0
LMI2C=	 0
LMS1C=	 0
LMS2C=	 0
NOME=	ABRIR / FECHAR DISJUNTOR 818
PAC=	S1_ATR1_818
PINT=	
RSULT=  SIM
TAC=	S1_TAC
TIPO=	PDS
TIPOE=	CTCL
TPCTL=	CSAC
TRRAC=  20
AOR=	CURSO
```

Salve o arquivo `CGS.dat` e execute `AtualizaBD fria fonte` para atualizar a base. 

**Dica:** erros de digitação como este são comuns! É sempre bom revisar com atenção os IDs e nomes para garantir que estão coerentes em todos os registros. 😉

Com essa correção, a base deve rodar sem problemas! 🤞

Se o erro persistir ou surgir outro problema, me avise e vamos investigar juntos! 😊
