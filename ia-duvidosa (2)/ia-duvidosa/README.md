# IA Duvidosa 🤥

Projeto de feira de ciências sobre desinformação e deepfakes. O visitante faz uma pergunta leve,
a IA escreve **duas respostas** (uma verdadeira e uma falsa, no mesmo tom confiante) e o visitante
tenta adivinhar qual é a verdadeira. Depois da escolha, o site mostra o que estava errado e como
checar a informação. Há um placar de acertos.

## Como funciona

- `index.html` é a página do site (o que as pessoas veem). O lado da resposta falsa (A ou B) é sorteado no navegador.
- A IA roda numa **função de servidor**, que guarda a sua chave em segredo. Nunca coloque a chave
  dentro do `index.html`, porque qualquer pessoa conseguiria copiá-la.
  - `netlify/functions/chat.mjs` é a função para a **Netlify** (junto com `netlify.toml`).
  - `api/chat.js` é a mesma função para a **Vercel**.
  - Você usa só uma das duas, conforme a hospedagem. A outra é ignorada.

## 1. Pegar uma chave de API gratuita (vale para as duas hospedagens)
1. Acesse https://aistudio.google.com e entre com uma conta Google.
2. Clique em **Get API key** e crie uma chave.
3. Guarde a chave. Não compartilhe com ninguém.

(Se você for menor de idade, peça ajuda a um responsável ou professor para criar a conta.)

## 2. Enviar o projeto para o GitHub
1. Crie um repositório no https://github.com.
2. Envie o **conteúdo** desta pasta (não a pasta em si) em **Add file > Upload files**.
   O `index.html`, o `netlify.toml`, a pasta `api` e a pasta `netlify` precisam ficar na raiz do repositório.

## 3A. Publicar na Netlify
**Atenção:** arrastar o zip ou a pasta para a Netlify publica só a página, sem a função da IA.
Isso causa o erro "Unexpected end of JSON input". Para a função funcionar, conecte o GitHub:

1. Em https://app.netlify.com clique em **Add new project > Import an existing project**.
2. Escolha **GitHub** e selecione o repositório.
3. Nas configurações, deixe o comando de build vazio e o diretório de publicação como `.` (o `netlify.toml` já informa isso).
4. Antes de publicar, abra **Environment variables** e crie `GEMINI_API_KEY` com a sua chave.
   (Se já publicou: **Project configuration > Environment variables**, e depois **Deploys > Trigger deploy**.)
5. Clique em **Deploy**. Abra o link gerado e teste uma pergunta.

Para mudar o endereço: **Project configuration > Domain management**. Domínio próprio também é possível aqui
(o domínio em si é comprado à parte, por exemplo no Registro.br).

## 3B. Publicar na Vercel
1. Em https://vercel.com entre com o GitHub e clique em **Add New > Project**.
2. Escolha o repositório.
3. Antes do **Deploy**, abra **Environment Variables** e crie `GEMINI_API_KEY` com a sua chave.
4. Clique em **Deploy** e abra o link gerado.

Para mudar o endereço: **Settings > Domains**.

## Personalizando

- **Comportamento da IA:** edite o texto `INSTRUCOES` na função da hospedagem que você usa
  (`netlify/functions/chat.mjs` ou `api/chat.js`). Se quiser manter as duas, altere nas duas.
- **Visual:** edite o `index.html`. As cores ficam no começo do arquivo, em `:root`.
- **Perguntas sugeridas:** procure a lista com a classe `sugestoes` no `index.html`.
- **Modelo:** se aparecer erro de modelo não encontrado, crie a variável `GEMINI_MODEL` na hospedagem
  com o nome de um modelo atual listado no Google AI Studio.

## Cuidados importantes

- O site avisa que parte do conteúdo é falso. Mantenha esse aviso visível.
- A IA está instruída a recusar temas sensíveis (saúde, política, pessoas reais). Não remova essas regras.
- A cota gratuita tem limite. Teste antes da feira e tenha um plano B (por exemplo, prints de rodadas prontas).
- Se a chave vazar, apague-a no Google AI Studio e crie outra.
