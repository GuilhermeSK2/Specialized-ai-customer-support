# Agente de Atendimento Especializado para Nobreak FXP-2000 (RAG)

Este projeto implementa um agente de inteligência artificial focado em atendimento ao cliente para o nobreak FXP-2000. Utilizando a arquitetura RAG (Retrieval-Augmented Generation), o agente combina o poder do modelo Gemini da Google com informações extraídas diretamente de um manual técnico em PDF (`manual_avancado_nobreak_fxp2000.pdf`). Isso permite que ele forneça respostas altamente precisas e contextualizadas sobre o produto.

## Visão Geral

A abordagem RAG é ideal para criar assistentes de IA que precisam de conhecimento específico que não está em seu treinamento geral. Neste projeto, o fluxo de trabalho é o seguinte:
1.  **Carregamento de Documentos:** O manual técnico do nobreak FXP-2000 é carregado e processado.
2.  **Geração de Embeddings e Vetorização:** O conteúdo do manual é convertido em representações numéricas (embeddings) usando `GoogleGenerativeAIEmbeddings` e armazenado em um banco de vetores FAISS. Isso permite uma busca eficiente por informações relevantes.
3.  **Criação do Retriever:** Um retriever é configurado para buscar os trechos mais relevantes do manual com base na pergunta do usuário.
4.  **Modelo de Linguagem (LLM):** O modelo Gemini (`gemini-2.5-flash`) é utilizado para processar a pergunta do usuário e as informações recuperadas.
5.  **Cadeia Conversacional:** `ConversationalRetrievalChain` do LangChain é empregada para gerenciar a conversa, incorporando o histórico do chat e as informações recuperadas para gerar respostas coerentes.
6.  **Assistente Especializado:** Um `SystemMessage` define o papel do agente como um especialista no nobreak FXP-2000, com instruções claras para responder a perguntas técnicas, de funcionalidade, garantia, manutenção, atualizações e suporte técnico.

## Estrutura do Projeto

* `AgenteRAGEspecializado.ipynb`: O notebook Jupyter que contém todo o código para as etapas de setup, carregamento de dados, construção do modelo RAG e a interface de chat.
* `manual_avancado_nobreak_fxp2000.pdf`: O arquivo PDF que serve como base de conhecimento para o agente. (Este arquivo deve ser fornecido ou ter uma instrução para download).

## Tecnologias Utilizadas

* **Python 3**
* **LangChain**: Framework para desenvolvimento de aplicações com LLMs.
    * `langchain_google_genai`: Integração com os modelos Gemini.
    * `langchain_community`: Componentes diversos, incluindo `FAISS` e `PyPDFLoader`.
    * `langchain_core`: Elementos básicos como `SystemMessage` e `RunnableWithMessageHistory`.
* **`faiss-cpu`**: Biblioteca para busca de similaridade em vetores.
* **`pypdf`**: Para carregar e extrair texto de arquivos PDF.
* **Google Gemini API**: Para o modelo de linguagem e embeddings.

## Pré-requisitos

1.  **API Key do Google Gemini:**
    * Acesse o Google AI Studio: [https://aistudio.google.com/](https://aistudio.google.com/)
    * Crie um novo projeto ou use um existente.
    * No menu lateral, clique em "Get API key".
    * Copie sua chave de API.
    * **Importante:** No notebook `AgenteRAGEspecializado.ipynb`, substitua `"Sua_Chave_Aqui"` pela sua chave de API real. Para maior segurança em projetos reais, considere usar variáveis de ambiente (e.g., com `python-dotenv`).

2.  **Arquivo PDF do Manual:**
    * Certifique-se de que o arquivo `manual_avancado_nobreak_fxp2000.pdf` esteja no mesmo diretório do notebook. Este é o documento que o agente usará como base de conhecimento.

## Interagindo com o Agente

Após executar todas as células, um prompt `Você:` aparecerá no seu terminal ou na saída do notebook. Você pode digitar suas perguntas sobre o nobreak FXP-2000. Digite `sair`, `quit` ou `exit` para encerrar a conversa.

**Exemplos de perguntas que você pode fazer:**
* "Qual a autonomia do nobreak?"
* "Existe um alarme sonoro de bateria fraca?"
* "E de falha interna?"
* "Como faço a manutenção do nobreak?"
* "Qual a voltagem de entrada?"
* "Para que serve a função ECO?"

## Contribuições

Contribuições são muito bem-vindas! Se você tiver sugestões para:
* Aprimorar a `SystemMessage` para refinar o comportamento do agente.
* Experimentar outras configurações de `ConversationalRetrievalChain` ou outros tipos de `retriever`.
* Integrar com diferentes tipos de fontes de dados (e.g., websites, bases de dados).
* Adicionar uma interface de usuário mais amigável.

Por favor, sinta-se à vontade para abrir uma issue ou enviar um pull request.

## Licença

Este projeto está licenciado sob a Licença MIT. Consulte o arquivo `LICENSE` para mais detalhes. (Se você não tiver um, pode criar um ou usar outra licença de sua preferência).
