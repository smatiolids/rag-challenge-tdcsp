# RAG Challenge no TDC São Paulo

Quer ganhar prêmios e um badge para publicar nas suas redes sociais e ainda praticar com o Langflow?

É muito simples! Basta usar o DataStax Langflow, criar um fluxo RAG e pronto!

![RAG Challenge - Badge](https://github.com/user-attachments/assets/a770ae91-7755-4c57-b507-dfd33077f5e2)

Quem completar o desafio e enviar a evidencia irá:

- Ganhar um **brinde** (sujeito a disponibilidade)
- Receber um Badge de reconhecimento
- Concorrer a **mochilas** sorteadas no fim do dia por volta das 17:30. (Fique de olho no seu email por volta deste horário)

Você só precisará de uma conta no **DataStax Astra** e na **OpenAI**

## Passo a passo

### Conta no Astra

Acesse o DataStax Astra em [datastax.astra.com](https://langflow.datastax.com?utm_medium=social_organic&utm_source=outreach&utm_campaign=tdcsp2024&utm_content=).

Se já tiver uma conta, tudo bem, é só acessá-la.

### Dados

Ao acessar o dashboard do **Astra**, encontre o botão "Create Database"

Escolha as opções:

- **Deployment type**: Serverless (Vector)
- **Database name**: langflow_tdc
- **Provider**: Amazon Web Services
- **Region**: us-east-2
  
![Criando o banco de dados](https://github.com/user-attachments/assets/6dde9c73-5b05-4ff1-9ec2-3a2bb1e2ac1b)

Pronto, vamos agora ao Langflow

### Langflow

No topo da tela, troque o contexto de "Astra DB" para "Langflow".

<img width="714" alt="Acessando o DataStax Langflow" src="https://github.com/user-attachments/assets/415fd653-2193-47a8-9e79-35686977f66a">

### Retrieval Augmented Generation

Vamos criar um fluxo **RAG**.

O **Retrieval Augmented Generation** envolve duas fases: 

1 - Carregar dados
2 - Utilizar as partes mais relevantes dos seus dados para ampliar o prompt.

Clique em "+ New Project" e escolha o template **"Vector Store RAG"**

<img width="1332" alt="Screenshot 2024-09-17 at 7 30 16 PM" src="https://github.com/user-attachments/assets/68916397-ea58-42e1-85fb-a5f6fedb1d08">

<img width="1168" alt="Screenshot 2024-09-17 at 7 32 46 PM" src="https://github.com/user-attachments/assets/ebf7d4e1-c42a-41f9-aea5-832ada044eef">

### Carregando dados

Localize este parte do fluxo, responsável por dividir um arquivo origem em "chunks", gerar um embedding para cada chunk e carregá-lo no Astra DB.

<img width="1610" alt="Screenshot 2024-09-17 at 7 34 18 PM" src="https://github.com/user-attachments/assets/f73876ae-bd4a-4ca4-93d0-9e9019815e15">

Faça os seguintes ajustes nos componentes;

- **"File"**: carregue o arquivo "Nike São Paulo Run 2024 _ Manual do Corredor.pdf", que está disponível aqui neste repositório.

- **"OpenAI Embeddings"**: informe a sua OpenAI API Key. Você pode criar uma variável global para reutilizar este valor. O modelo de embedding utilizado será o padrão: text-embedding-3-small.

- **"Astra DB"**: escolha o "Database" (se você seguiu as instruções deve ser "langflow_tdc") e, em seguida, no campo Collection, selecione "Create a new collection".

- - **Collection Name**: "langflow_nike_run"
- - **Dimensions**: 1536
- - **Metric**: cosine
  
<img width="557" alt="Screenshot 2024-09-17 at 7 40 29 PM" src="https://github.com/user-attachments/assets/18356a5c-30ab-4651-bb0e-aaa9820066c5">

Com isso, sua collection será criada.

Clique no botão "play" no componente Astra DB.

Deve ficar tudo verdinho assim:

<img width="1329" alt="Screenshot 2024-09-17 at 7 43 30 PM" src="https://github.com/user-attachments/assets/fa32e6f3-4887-45f1-8187-717f2f0b0848">

Volte ao Astra, e confira os dados:

<img width="1272" alt="Screenshot 2024-09-17 at 7 44 46 PM" src="https://github.com/user-attachments/assets/bfd50d07-2c11-4590-bd51-b5fa8fb532ac">

Visualizando os dados JSON, algo assim:

<img width="1006" alt="Screenshot 2024-09-17 at 7 45 37 PM" src="https://github.com/user-attachments/assets/f99bad33-6e08-418e-8002-5fb2879ed428">

Dados carregados, vamos à segunda parte do RAG.

### Ampliando o prompt

Voltando ao Langflow, abra o fluxo criado e localize o componente Chat Input. Ele é o início do fluxo de interação entre usuário, dados e modelo de linguagem.

<img width="1498" alt="Screenshot 2024-09-17 at 7 48 33 PM" src="https://github.com/user-attachments/assets/09e2fed9-f075-4eab-be69-357db0e766df">

Ajustes por componente:

- "OpenAI Embedding": O model deve ser o text-embedding-3-small e a OpenAI API Key deve estar preenchida com uma variável de ambiente ou com o próprio valor da sua chave.
- "Astra DB": Escolha novamente o "Database"(mesmo anterior) e a collection "langflow_nike_run".
- "Prompt": Aqui não precisa alterar nada, mas você poderia acrescentar instruções ao modelo ajustando este prompt ou passando variáveis adicionais.
- "OpenAI": Aqui é o componente que configura o modelo LLM a ser utilizado. Você pode mudar o modelo se quiser, mas confirme se a OpenAI API Key está preenchida.

Pronto, é só rodar!

Clique no botão Playground e faça perguntas sobre esta corrida. Sugestões:

- De onde sai a corrida de 5km?
- Tem guarda volumes?
- Qual a hora da largada dos 10km?
- Haverá agua disponivel?
- Onde é a chegada?
- Onde é a termina?

Terminou? Legal, agora é so mandar o url do seu fluxo pelo form abaixo e passar no nosso estande!

O URL está aqui:
<img width="1027" alt="Screenshot 2024-09-17 at 7 58 21 PM" src="https://github.com/user-attachments/assets/6dc02d4d-c70a-4d3d-b871-43dbfac20d33">

Formulário para envio: https://forms.gle/hDfcaU8cJXQhrDcq7

# Curtiu?

Mande seu feedback para: samuel.matioli@datastax.com

# Condições gerais

- Brindes sujeitos à disponibilidade
- 4 Mochilas sorteadas por dia
- Retirada dos brindes será somente presencial.










