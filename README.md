# Assistente Inteligente para Configuração do SAGE
Repositório com links e material suplementar do trabalho apresentado no XVII STPC. O artigo está disponível para download no seguinte link: [Artigo STPC](./arquivos/XVII_STPC_IT_Assistente_Sage.pdf).


 ## Protótipo SageLM

 Uma implementação experimental do assistente, batizada de SageLM, está disponível no seguinte link: [SageLM](https://sagelm.onrender.com).

O assistente foi desenvolvido em python utilizando a biblioteca streamlit e a API do Gemini da Google. Para utilizá-lo é necessário ter uma conta do Google e [gerar uma chave de API do Gemini](https://aistudio.google.com/app/apikey).

Um tutorial de como utilizar o SageLM está disponível no seguinte link: [Tutorial SageLM](./arquivos/Tutorial_SageLM.pdf).

## Avaliação dos especialistas

A pesquisa com especialistas em Sage foi realizada com 13 profissionais. Cada um avaliou pares de perguntas e respectivas respostas geradas pelo Gemini 1.5 Pro. Os especialistas foram instruídos a avaliar a qualidade das respostas do Gemini em termos de corretude, clareza e relevância, dando uma nota de 1 a 10 para cada uma. Para o caso de respostas que não atendiam aos critérios estabelecidos, os especialistas foram instruídos a fazer comentários para complementar ou indicar quais seriam as respostas corretas.

As respostas coletadas estão disponíveis em [arquivos/pesquisa.xlsx](./arquivos/pesquisa.xlsx).


## Dados de treinamento

Os pares de perguntas e respostas avaliados pelos especialistas foram amostrados da base completa de 1740 perguntas e respostas geradas com o Gemini 1.5 Pro cobrindo assuntos relacionados à configuração de base fonte SCADA do SAGE, incluindo configurações específicas para IEC 61850, ICCP e DNP. Esta base sofreu ajustes após a avaliação dos especialistas e está disponível como um lista json em [arquivos/qa.json](./arquivos/qa.json).

O conjunto de perguntas e respostas também está disponível em formato de treinamento para o GPT no Hugging Face em [pascarujo/sage-qa-training/](https://huggingface.co/datasets/pascarujo/sage-qa-training).


## Como treinar o gpt-4o

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

## Como treinar o Gemini

Você deve entrar no Google AI Studio e selecionar [New Tuned Model](https://aistudio.google.com/fine-tuning) no menu lateral esquerdo. Em Select data for tuning, carregue o [arquivo xlsx de treinamento](./arquivos/qa.xlsx) selecionando `Importar > Upload`. Após o arquivo ser carregado, você precisará selecionar quais colunas do arquivo contém as perguntas e respostas para treinamento, conforme a imagem abaixo:

![Seleção de colunas](./img/gemini-fine-tuning-01.jpj)


