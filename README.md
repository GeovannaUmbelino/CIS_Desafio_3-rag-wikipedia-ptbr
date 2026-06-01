#  RAG - Wikipedia PT/BR 

Este repositório contém a solução para o **Desafio 3** do CIS. O projeto implementa um pipeline completo de **Retrieval-Augmented Generation (RAG)** em linguagem natural (PT-BR) utilizando artigos da Wikipedia como base de conhecimento.

O sistema recupera informações relevantes de uma base indexada e utiliza um modelo LLM (Large Language Model) para formular respostas precisas, evitando alucinações.

---

## 🚀 Funcionalidades e Atividades Realizadas

- **✅ Atividade Obrigatória:** Pipeline RAG funcional utilizando o dataset `wikimedia/wikipedia` (20231101.pt) consumido via biblioteca `datasets`.
- **✅ Atividade Opcional (a):** Pré-processamento e _chunking_ dos artigos com limite de tamanho e _overlap_ inteligente para preservar o contexto das frases.
- **✅ Atividade Opcional (b):** Geração de _Embeddings_ (vetorização semântica) utilizando o modelo open-source `all-MiniLM-L6-v2` e indexação de alta performance para busca por similaridade utilizando **FAISS**.
- **✅ Atividade Opcional (c):** Integração com o LLM `google/flan-t5-base` para geração de respostas com injeção de contexto no prompt, além da comparação qualitativa entre abordagens *Closed-book* (sem RAG) e com RAG.

---

## 🛠️ Tecnologias Utilizadas

O ambiente principal de desenvolvimento foi o **Google Colab** (GPU T4), utilizando as seguintes bibliotecas Python:

* `datasets`
* `transformers` 
* `sentence-transformers` 
* `faiss-cpu` 
* `torch` 

---

## ⚙️ Como Executar o Projeto

1. Acesse o [Google Colab](https://colab.research.google.com/).
2. Faça o upload do arquivo `rag_wikipedia_ptbr(2).ipynb`.
3. Vá em **Runtime** -> **Change runtime type** e certifique-se de que o acelerador de hardware **T4 GPU** está selecionado.
4. Execute todas as células sequencialmente. O primeiro bloco de código fará a instalação de todas as dependências necessárias.

---

## 📊 Análise Qualitativa

### 1. Comparativo de Respostas (RAG vs No-RAG)
Durante a avaliação, testamos a pergunta: **"Quem foi Dom Pedro II?"**

* **Sem RAG (Closed-book):** O modelo fornece uma resposta genérica, imprecisa ou em outro idioma por não possuir o conhecimento consolidado em seus pesos.
* **Com RAG:** O modelo retorna uma resposta historicamente correta e rica em detalhes, embasada exclusivamente nos textos recuperados da Wikipedia através da busca vetorial.

### 2. Impacto do Tamanho do Chunk
Durante os testes, observou-se que alterar o tamanho dos chunks (ex: 128 vs 256 vs 512 tokens) afeta diretamente a recuperação:

* **Chunks menores (ex: 128):** Trazem trechos muito específicos, mas correm o risco de perder o contexto geral da frase, prejudicando a formulação da resposta do LLM.
* **Chunks maiores (ex: 512):** Garantem que o LLM receba uma ideia completa, mas podem diluir a relevância da busca vetorial no FAISS, trazendo informações desnecessárias na mesma janela de contexto. O tamanho de 256 com overlap de 30 provou ser um meio-termo ideal para este projeto.

---

Desenvolvido por [Geovanna Alves Umbelino](https://github.com/GeovannaUmbelino) 
