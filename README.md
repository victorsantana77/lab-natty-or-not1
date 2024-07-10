# Processamento de Linguagem Neural com Python

## 📒 Descrição
Este projeto explora o uso de redes neurais no Processamento de Linguagem Natural (PLN), uma subárea da inteligência artificial que lida com a interação entre computadores e seres humanos através da linguagem natural. O objetivo do PLN é permitir que as máquinas compreendam, interpretem e respondam à linguagem humana de maneira valiosa e útil, abrangendo tarefas como tradução automática, análise de sentimentos, geração de texto e resposta a perguntas.

## 🤖 Tecnologias Utilizadas
- [Transformers](https://huggingface.co/transformers/)
- [PyTorch](https://pytorch.org/)
- [Hugging Face](https://huggingface.co/)

## 🧐 Processo de Criação

### Instalação da Biblioteca `transformers`
Primeiro, precisamos instalar a biblioteca `transformers` da Hugging Face e outras dependências necessárias, como `torch` para PyTorch:

```python
!pip install transformers torch
```

### Carregando um Modelo Pré-treinado
Carregamos um modelo pré-treinado e seu tokenizador correspondente. Neste exemplo, usamos o modelo `distilbert-base-uncased`, uma versão mais leve do BERT:

```python
from transformers import DistilBertTokenizer, DistilBertModel

# Carregar o tokenizador e o modelo
tokenizer = DistilBertTokenizer.from_pretrained('distilbert-base-uncased')
model = DistilBertModel.from_pretrained('distilbert-base-uncased')
```

### Tokenização de Texto
A tokenização é o processo de dividir o texto em unidades menores (tokens). No contexto do PLN, isso geralmente significa dividir o texto em palavras ou sub-palavras que o modelo pode entender:

```python
# Texto de exemplo
text = "Natural language processing with neural networks is fascinating."

# Tokenizar o texto
inputs = tokenizer(text, return_tensors='pt')
print(inputs)
```

### Passando os Tokens pelo Modelo
Uma vez que o texto tenha sido tokenizado, podemos passar os tokens pelo modelo para obter as representações embutidas (embeddings):

```python
# Passar os tokens pelo modelo
outputs = model(**inputs)

# Extrair as representações embutidas
embeddings = outputs.last_hidden_state
print(embeddings)
```

### Aplicações Comuns

1. **Análise de Sentimentos:**
   Podemos usar modelos pré-treinados para classificar o sentimento de um texto.

2. **Geração de Texto:**
   Modelos como GPT podem ser usados para gerar texto a partir de um prompt.

3. **Resposta a Perguntas:**
   Modelos como BERT podem ser ajustados para responder a perguntas baseadas em um contexto fornecido.

### Exemplo de Análise de Sentimentos
Para um exemplo completo de análise de sentimentos, podemos usar o pipeline da Hugging Face, que facilita a execução de tarefas específicas de PLN:

```python
from transformers import pipeline

# Criar um pipeline de análise de sentimentos
sentiment_pipeline = pipeline('sentiment-analysis')

# Texto de exemplo
text = "I love natural language processing!"

# Analisar o sentimento
result = sentiment_pipeline(text)
print(result)
```
### Exemplos e Insights

Aqui estão alguns exemplos e insights sobre o uso de redes neurais em Processamento de Linguagem Natural (PLN):

- [Análise de Sentimentos](https://github.com/huggingface/notebooks/blob/master/examples/sentiment_analysis.ipynb)
- [Geração de Texto](https://github.com/huggingface/notebooks/blob/master/examples/text_generation.ipynb)
- [Resposta a Perguntas](https://github.com/huggingface/notebooks/blob/master/examples/question_answering.ipynb)

### Links Interessantes

1. **Hugging Face: Transformers Documentation**
   - [Documentação dos Transformers](https://huggingface.co/transformers/)
   - Esta documentação fornece informações detalhadas sobre como usar a biblioteca `transformers` para várias tarefas de PLN.

2. **Kaggle: Natural Language Processing with Disaster Tweets**
   - [Competição Kaggle](https://www.kaggle.com/c/nlp-getting-started)
   - Esta competição oferece uma excelente oportunidade para praticar PLN, utilizando redes neurais para classificar tweets sobre desastres.

3. **Towards Data Science: An Overview of BERT and GPT-2**
   - [Artigo sobre BERT e GPT-2](https://towardsdatascience.com/an-overview-of-bert-and-gpt-2-2c1f87f6b76e)
   - Este artigo explica os conceitos e avanços por trás dos modelos BERT e GPT-2, além de fornecer exemplos práticos.

4. **Google AI Blog: BERT Explained**
   - [BERT Explicado](https://ai.googleblog.com/2018/11/open-sourcing-bert-state-of-art-pre.html)
   - Um artigo detalhado sobre o modelo BERT, incluindo sua arquitetura e como ele melhorou o estado da arte em várias tarefas de PLN.

5. **ArXiv: Attention Is All You Need**
   - [Paper sobre Transformadores](https://arxiv.org/abs/1706.03762)
   - O artigo original que introduziu os transformadores, revolucionando o campo do PLN e estabelecendo a base para modelos como BERT e GPT.


## 🚀 Resultados
Os resultados deste projeto demonstram como as redes neurais podem ser usadas para analisar e gerar linguagem natural de maneira eficaz. Utilizando a biblioteca `transformers` da Hugging Face, conseguimos realizar tarefas complexas com apenas algumas linhas de código.

## 💭 Reflexão (Opcional)
Trabalhar com PLN e redes neurais foi um desafio interessante, mostrando o poder das tecnologias modernas em entender e manipular a linguagem humana. As ferramentas disponíveis hoje facilitam a implementação de soluções avançadas, oferecendo grandes possibilidades para desenvolvedores e pesquisadores na área de inteligência artificial.
