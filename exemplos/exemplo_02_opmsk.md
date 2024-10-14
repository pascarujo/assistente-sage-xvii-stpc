**Usuário:** preciso de ajuda para configurar o opmsk de um IED.

---

**Assistente:** Com prazer, posso te ajudar a configurar o OPMSK do seu IED! 😊

Para te dar uma mãozinha, preciso de algumas informações. Me fale sobre a sua configuração:

1. O IED suporta a criação de datasets dinâmicos pelo SAGE? Se sim, podemos desligar o bit responsável por essa funcionalidade no OPMSK.

2. Você está utilizando GOOSE para receber dados do IED? Se não, podemos desligar o bit relacionado ao GOOSE.

3. Como estão configurados os Report Control Blocks do seu IED? Eles estão configurados individualmente em cada Logical Node, ou estão centralizados no LLN0? Essa informação é importante para configurar o bit que define qual RCB o SAGE deve utilizar.

4. Você prefere que o SAGE receba os dados do IED apenas quando houver mudança no valor do ponto, ou também quando houver mudança na qualidade do dado? Essa preferência define o trigger dos reports e, consequentemente, o bit correspondente no OPMSK.

5. Você deseja forçar a checagem de intertravamento independente das configurações de CGF?

6. O IED é redundante? Se sim, o bit de redundância no OPMSK deverá ser ligado.

7. Por último, você deseja que o IED envie os identificadores das varáveis nos Reports? 

Com base nessas informações, podemos definir quais bits do OPMSK devem ser ligados ou desligados para atender a sua necessidade! 💪

Aguardo pelas suas respostas para que possamos configurar o OPMSK! 😄


---

**Usuário:** o IED não suporta datasets dinâmicos. não estou usando goose. os reports não estão no LLN0. quero que os dados sejam reportados na mudança de valor ou qualidade. o IED não é redundante. habilite os ids nos reports e force o intertravamento. também ligue o bit 15.

---

**Assistente:** Maravilha, você me deu todas as informações que eu precisava! 🎉

Com base no que você me disse, a configuração do OPMSK para o seu IED ficaria assim:

- **Bit 4 (datasets dinâmicos):** Ligado, pois o IED não suporta datasets dinâmicos. O SAGE terá que usar os datasets pré-configurados no IED.

- **Bit 5 (Report Control Blocks no LLN0):** Desligado, já que os reports não estão configurados no LLN0.

- **Bit 6 (ativação de GOOSE):** Desligado, pois você não está utilizando GOOSE.

- **Bit 8 (uso de InterLockCheck):** Ligado, para forçar a checagem de intertravamento independente do KCONV.

- **Bit 9 (trigger dos reports):** Desligado, para que o SAGE receba dados quando houver mudança no valor ou qualidade do ponto.

- **Bit 12 (redundância):** Desligado, pois o IED não é redundante.

- **Bit 15 (time-tags inválidos):** Ligado, o SAGE deve ignorar os atributos de invalidade em time-tags.

- **Bit 20 (opção de DataReference no Report Control Block):** Ligado, o IED deve enviar a identificação dos pontos nos Reports.

- **Demais bits:** Desligados por padrão.

Representando em binário, a máscara ficaria: `0001 0000 1000 0001 0001 0000`

```python

print(hex(int('000100001000000100010000', 2)))
```

```Code execution output
0x108110
```

Este valor binário corresponde ao valor hexadecimal **108110**. Basta substituir `<OPMSK>` no seu arquivo `CNF.dat` por `108110`.

Após a alteração, salve o arquivo e execute `AtualizaBD fria fonte` para atualizar a base de dados do SAGE.

Pronto! 🎉 Com essa configuração, o SAGE deve se comunicar com o seu IED utilizando as opções que você definiu. Se tiver mais alguma dúvida, pode me perguntar. 😊






