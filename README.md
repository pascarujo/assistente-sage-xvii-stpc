# Assistente Inteligente para Configuração do SAGE
Repositório com links e material suplementar do trabalho apresentado no XVII STPC. O artigo está disponível para download no seguinte link: [Artigo STPC](./arquivos/XVII_STPC_IT_Assistente_Sage.pdf).


 ## 🚀 Protótipo SageLM

 Uma implementação experimental do assistente, batizada de SageLM, está disponível no seguinte link: [SageLM](https://sagelm.onrender.com).

O assistente foi desenvolvido em python utilizando a biblioteca streamlit e a API do Gemini da Google. Para utilizá-lo é necessário ter uma conta do Google e [gerar uma chave de API do Gemini](https://aistudio.google.com/app/apikey).

Um tutorial de como utilizar o SageLM está disponível no seguinte link: [Tutorial SageLM](./arquivos/Tutorial_SageLM.pdf).

## 🔎 Avaliação dos especialistas

A pesquisa com especialistas em Sage foi realizada com 13 profissionais. Cada um avaliou pares de perguntas e respectivas respostas geradas pelo Gemini 1.5 Pro. Os especialistas foram instruídos a avaliar a qualidade das respostas do Gemini em termos de corretude, clareza e relevância, dando uma nota de 1 a 10 para cada uma. Para o caso de respostas que não atendiam aos critérios estabelecidos, os especialistas foram instruídos a fazer comentários para complementar ou indicar quais seriam as respostas corretas.

As respostas coletadas estão disponíveis em [arquivos/pesquisa.xlsx](./arquivos/pesquisa.xlsx).


## 📚 Dados de treinamento

Os pares de perguntas e respostas avaliados pelos especialistas foram amostrados da base completa de 1740 perguntas e respostas geradas com o Gemini 1.5 Pro cobrindo assuntos relacionados à configuração de base fonte SCADA do SAGE, incluindo configurações específicas para IEC 61850, ICCP e DNP. Esta base sofreu ajustes após a avaliação dos especialistas e está disponível como um lista json em [arquivos/qa.json](./arquivos/qa.json).

O conjunto de perguntas e respostas também está disponível em formato de treinamento para o GPT no Hugging Face em [pascarujo/sage-qa-training/](https://huggingface.co/datasets/pascarujo/sage-qa-training).


## 🧠 Treinando o gpt-4o

Você deve logar na área de API da OpenAI e selecionar [Fine-Tuning](https://platform.openai.com/finetune/) no Dashboard. Clique em Create no canto superior direito e selecione o modelo gpt-4o-mini ou outro do seu interesse. Carregue o [arquivo de treinamento](https://huggingface.co/datasets/pascarujo/sage-qa-training), escolha um identificador para o fine-tuning em `Suffix` e selecione as opções de configuração para criar o fine-tuning:

- **Seed**: número aleatório para inicializar o algoritmo de treinamento. Especificar o mesmo valor de seed e dos outros parâmetros de configuração facilita a reprodução dos resultados.
- **Batch size**: número de exemplos por lote de treinamento.
- **Learning rate multiplier**: multiplicador da taxa de aprendizado.
- **Number of epochs**: número de épocas de treinamento, ou seja, quantas vezes o algoritmo verá todo o conjunto de treinamento.

Você pode deixar em branco os campos acima e utilizar os valores padrão, mas é recomendado testar diferentes configurações para encontrar a que apresenta melhor desempenho. Você pode ler mais sobre os parâmetros de configuração [aqui](https://platform.openai.com/docs/guides/fine-tuning/).

Após preencher os campos, clique em `Create`.

Um dos testes de fine-tuning realizados com o gpt-4o-mini utilizou os seguintes parâmetros:

- Batch size: 1
- Learning rate multiplier: 0.1
- Number of epochs: 4
- Seed: 132787610

Usando a base de treinamento, o fine-tuning levou aproximadamente 4,5 hora para ser concluído, treinando um total de `1.542.188` tokens. Observe que existe um custo para treinamento de modelos, você pode ter mais detalhes [aqui](https://openai.com/api/pricing/).

## 🧠 Treinando o Gemini

Você deve entrar no Google AI Studio e selecionar [New Tuned Model](https://aistudio.google.com/fine-tuning) no menu lateral esquerdo. Em Select data for tuning, carregue o [arquivo xlsx de treinamento](./arquivos/qa.xlsx) selecionando `Importar > Upload`. Após o arquivo ser carregado, você precisará selecionar quais colunas do arquivo contém as perguntas e respostas para treinamento, conforme a imagem abaixo:

![gemini-fine-tuning-01](https://github.com/user-attachments/assets/5bb56520-a871-4c47-b021-a46aa307c912)

Marque a opção `Use first row as header` e clique em `Importar`.
Após a importação do treinamento, defina os demais parâmetros de configuração:

- Tuned model name: nome do modelo treinado.
- Choose base model: selecione o modelo base para o treinamento (gemini-1.5-flash-tuning foi o usado neste trabalho).
- Em Advanced settings, você pode alterar os parâmetros de configuração do treinamento, similar ao que foi feito para o gpt-4o-mini, mas é possível deixar com os valores padrão. Clique em `Tune` para iniciar o treinamento.

Um dos testes de fine-tuning realizados com o Gemini 1.5 Flash utilizou os seguintes parâmetros:

- Choose base model: `gemini-1.5-flash-tuning`
- Batch size: 8
- Learning rate multiplier: 0.0002 
- Number of epochs: 4

Saiba mais sobre o fine-tuning no Gemini [aqui](https://ai.google.dev/gemini-api/docs/model-tuning/).

 
## 🐑 Treinando o Llama 3.1 8B

O modelo Llama 3.1 8B é um modelo open source da Meta baseado em LlamA 3.1, mas com apenas 8 bilhões de parâmetros. Ele pode ser treinado utilizando diversas plataformas e métodos, mas neste trabalho foi usado a biblioteca [Unsloth](https://github.com/unslothai/unsloth).

O notebook usado para o treinamento está em [notebooks/sage_llama.ipynb](https://github.com/pascarujo/assistente-sage-xvii-stpc/blob/main/notebooks/sage_llama.ipynb)

O modelo treinado está disponível no Hugging Face em [pascarujo/SageLlama-3.1-8B-GGUF](https://huggingface.co/pascarujo/SageLlama-3.1-8B-GGUF).


## ⭐ Assistente utilizando o Gemini

Um código de teste para utilizar o Gemini 1.5 Flash como um assistente de configuração do Sage está disponível em [notebooks/assistente_gemini.ipynb](https://github.com/pascarujo/assistente-sage-xvii-stpc/blob/main/notebooks/assistente_gemini.ipynb).

Para utilizar o código, é necessário:

- [Gerar uma chave de API do Gemini](https://aistudio.google.com/app/apikey).
- Definir os arquivos que serão utilizados como base de conhecimento para in-context learning. Por padrão, os arquivos devem ficar na pasta dados. Como teste, você pode usar os exemplos de perguntas e respostas disponíveis em [arquivos/qa.xlsx](./arquivos/qa.xlsx).
- Definir o prompt de instrução que será utilizado para o modelo. Um exemplo simples está disponível no notebook.

Observe que esta é uma versão simplificada do assistente. 

## 📧 Exemplos de uso do assistente

Por questão de espaço, apenas alguns exemplos de conversação com o assistente foram inseridos no artigo. No diretório exemplos está o resultado de diversos testes de interação com o protótipo:

- [Exemplo 01 - Erro de digitação no ID do CGS](./exemplos/exemplo_01_erro_digitação.md)
- [Exemplo 02 - Ajuda na configuração do OPMSK](./exemplos/exemplo_02_opmsk.md)
- [Exemplo 03 - Ajuda para clonar uma base](./exemplos/exemplo_03_duplicação_de_pontos.md)
- [Exemplo 04 - Tirando dúvidas de um iniciante](./exemplos/exemplo_04_iniciante.md)
- [Exemplo 05 - Descrevendo tabelas](./exemplos/exemplo_05_descrição_tabelas.md)
- [Exemplo 06 - Criando um diagrama](./exemplos/exemplo_06_criar_diagrama.md)
- [Exemplo 07 - Resposta a pergunta da base de treinamento](./exemplos/exemplo_07_melhora_na_resposta.md)
- [Exemplo 08 - Visão geral do Sage](./exemplos/exemplo_08_visao_geral.md)
- [Exemplo 09 - Teste de alinhamento](./exemplos/exemplo_09_alinhamento.md)
- [Exemplo 10 - Explicação lúdica](./exemplos/exemplo_10_lúdico.md)
- [Exemplo 11 - Conhecimento especialista](./exemplos/exemplo_11_conhecimento_especialista.md)
- [Exemplo 12 - Rede de difusão confiável](./exemplos/exemplo_12_difusao_confiavel.md)

## 📖 Referências

- [Attention is all you need](https://arxiv.org/abs/1706.03762)
- [Language Models are Few-Shot Learners](https://arxiv.org/abs/2005.14165)
- [Chain-of-Thought Prompting Elicits Reasoning in Large Language Models](https://arxiv.org/abs/2201.11903)
- [Parameter-Efficient Transfer Learning for NLP](https://arxiv.org/abs/1902.00751)
- [LoRA: Low-Rank Adaptation of Large Language Models](https://arxiv.org/abs/2106.09685v1)
- [Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks](https://arxiv.org/abs/2005.11401)
- [A Survey on Knowledge Graphs: Representation, Acquisition, and Applications](https://arxiv.org/abs/2002.00388v2)
- [From Local to Global: A Graph RAG Approach to Query-Focused Summarization](https://arxiv.org/abs/2404.16130)
- [A modular graph-based Retrieval-Augmented Generation (RAG) system](https://github.com/microsoft/graphrag)
- [On the Opportunities and Risks of Foundation Models](https://arxiv.org/abs/2108.07258)


