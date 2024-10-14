**Assistente:** Como posso ajudá-lo?

---

**Usuário:** você pode me ajudar com alguns valores de OPMSK usados normalmente em IEDs da Siemens?

---

**Assistente:** Claro! Para IEDs Siemens, os valores do OPMSK mais comuns variam de acordo com a família.

- **SIPROTEC 4:**
  - Para datasets pré-definidos: `28020` ou `28420`
  - Para datasets dinâmicos (se o IED suportar): `28220` ou `28620`
- **SIPROTEC 5:**
  - Para datasets pré-definidos: `228420` ou `228227`
  - Para datasets dinâmicos (se o IED suportar): `228220` ou `228627`

Lembre-se que estas são apenas algumas sugestões comuns. A melhor forma de determinar o valor correto do OPMSK é consultar a documentação do seu IED específico, incluindo os arquivos XML de configuração (ICD ou SCD), e usar a ferramenta xml61850 para gerar a base do SAGE.

**Dicas:**

- **Verifique se o IED suporta datasets dinâmicos**. Se sim, você precisa ativar o bit 4 do OPMSK.
- **Use a ferramenta xml61850 para gerar a base do SAGE**. Esta ferramenta pode ajudar a determinar o valor correto do OPMSK com base na configuração do IED.

Em caso de dúvidas, consulte o manual do SAGE ou a documentação específica do seu IED.