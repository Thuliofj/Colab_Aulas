# 📓 Colab_Aulas

Repositório com os **notebooks das aulas** que faço no Google Colab durante meus estudos de **Python e Análise de Dados** (bootcamp da Generation Brasil). Cada notebook é uma aula prática, com explicações em português e código pronto para executar no navegador, sem instalar nada.

O tema até agora é **APIs**: começo consumindo APIs prontas (fotos de cachorros e gatos) e termino criando a minha própria, usando o Google Sheets.

![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)
![Google Colab](https://img.shields.io/badge/Google%20Colab-F9AB00?logo=googlecolab&logoColor=white)
![Google Sheets](https://img.shields.io/badge/Google%20Sheets-34A853?logo=googlesheets&logoColor=white)

## 🗺️ Meu progresso

```
🐶 dog  →  🐱 cat  →  🏁 desafio_01  →  🏁 desafio_02  →  💬 mensagens
 uma        uma         várias           galeria HTML      minha própria
 imagem     imagem      imagens          Cães vs Gatos     API (Sheets)
```

| # | Notebook | Tema | O que aprendi | Abrir |
|---|---|---|---|---|
| 1 | [`dog.ipynb`](api/dog.ipynb) | 🐶 Uma imagem de cachorro | Primeira requisição `GET`, ler o JSON da resposta, baixar e salvar uma imagem | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Thuliofj/Colab_Aulas/blob/main/api/dog.ipynb) |
| 2 | [`cat.ipynb`](api/cat.ipynb) | 🐱 Uma imagem de gato | Mesmo fluxo com outra API, percebendo que cada API devolve o JSON em um formato diferente | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Thuliofj/Colab_Aulas/blob/main/api/cat.ipynb) |
| 3 | [`desafio_01.ipynb`](api/desafio_01.ipynb) | 🐶🐱 Várias imagens | Parâmetros de URL, laço com `enumerate`, função `salvar()` e nomes de arquivo diferentes | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Thuliofj/Colab_Aulas/blob/main/api/desafio_01.ipynb) |
| 4 | [`desafio_02.ipynb`](api/desafio_02.ipynb) | 🐶 vs 🐱 Galeria | Gerar uma página `galeria.html` com Python, imagens em base64 e arquivo `.zip` para download | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Thuliofj/Colab_Aulas/blob/main/api/desafio_02.ipynb) |
| 5 | [`mensagens.ipynb`](api/mensagens.ipynb) | 💬 API própria com Google Sheets | Criar uma API com Apps Script e conversar com ela usando `POST` e `GET` | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Thuliofj/Colab_Aulas/blob/main/api/mensagens.ipynb) |

## 📂 Estrutura

```
Colab_Aulas/
├── api/
│   ├── dog.ipynb
│   ├── cat.ipynb
│   ├── desafio_01.ipynb
│   ├── desafio_02.ipynb
│   └── mensagens.ipynb
└── README.md
```

## ▶️ Como executar qualquer notebook

1. Clique no botão **Open In Colab** do notebook.
2. Execute as células **de cima para baixo** (botão de play ao lado da célula ou `Shift + Enter`).
3. O Colab já traz Python e a biblioteca `requests`, então não precisa instalar nada.

> ⚠️ No Colab os arquivos ficam em `/content` e **são apagados quando a sessão termina**. Baixe o que quiser guardar pelo painel de arquivos (ícone de pasta, à esquerda).

---

## 📘 Detalhes de cada etapa

### 1 e 2 · `dog.ipynb` e `cat.ipynb` — consumindo APIs prontas

Os dois notebooks seguem o mesmo roteiro: fazer uma requisição, ler o endereço da imagem no JSON, baixar e exibir.

| | 🐶 Cachorro | 🐱 Gato |
|---|---|---|
| API | [Dog CEO](https://dog.ceo/dog-api/) | [The Cat API](https://thecatapi.com/) |
| Endereço da imagem no JSON | `data['message']` | `data[0]['url']` |
| Arquivo salvo | `imagens/dog/dog.jpg` | `imagens/cat/cat.jpg` |

**Aprendizado:** cada API organiza a resposta de um jeito. A do cachorro devolve um objeto, a do gato devolve uma lista, então é preciso olhar o JSON antes de acessar o dado.

### 3 · `desafio_01.ipynb` — várias imagens

Pede várias imagens de uma vez e salva cada uma com um nome diferente (`dog_1`, `dog_2`, `cat_1`...) em `imagens/multiplas/`.

- Cachorros: a API aceita `/random/N` na própria URL.
- Gatos: a API aceita o parâmetro `?limit=N`.
- Uma função `salvar(img_url, nome)` evita repetir o código de download.

### 4 · `desafio_02.ipynb` — galeria "Cachorros vs Gatos"

Baixa 6 imagens de cada animal e gera uma página `galeria.html` com duas colunas lado a lado.

- A função `gerar_html(src)` recebe outra função que decide o endereço de cada `<img>`. Assim o mesmo código gera a versão para download (caminhos relativos) e a versão exibida no notebook (imagens embutidas em base64).
- No final, cria um `galeria.zip` com a página e as imagens, pronto para abrir no navegador.

---

## 🚀 Destaque: `api/mensagens.ipynb` (minha API própria)

### A ideia

Uma API normalmente exige servidor, banco de dados e hospedagem. Aqui o desafio foi **montar uma API própria usando só ferramentas gratuitas do Google**:

- **Google Sheets** funciona como o banco de dados.
- **Google Apps Script** transforma a planilha em uma pequena API web (`doPost` e `doGet`).
- **Python + `requests`** conversa com essa API direto do Colab.

```
Notebook (Python)  ──POST──▶  Apps Script (doPost)  ──▶  grava uma linha na planilha
Notebook (Python)  ◀──GET───  Apps Script (doGet)   ◀──  lê as linhas da planilha
```

### Funções do notebook

| Função | Método HTTP | O que faz |
|---|---|---|
| `enviar_mensagem(nome, email)` | `POST` | Envia uma mensagem para a planilha |
| `enviar_varias_mensagens(mensagens)` | `POST` | Envia uma lista de mensagens, uma por uma |
| `obter_todas_mensagens()` | `GET` | Busca todas as linhas da planilha em JSON |
| `obter_ultima_mensagem()` | `GET` | Busca somente a mensagem mais recente |

### Exemplo de resposta

As chaves vêm dos cabeçalhos da planilha (`Data`, `Nome` e `Email`):

```json
{
  "Data": "2026-11-04T18:18:53.000Z",
  "Nome": "charlie",
  "Email": "charlie@example.com"
}
```

### 🛠️ Como montar a sua versão

1. Crie uma planilha no Google Sheets e coloque na linha 1 os cabeçalhos: `Data`, `Nome`, `Email`.
2. Abra **Extensões → Apps Script** e cole um código como este (exemplo):

   ```javascript
   function doPost(e) {
     const aba = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
     const dados = JSON.parse(e.postData.contents);
     aba.appendRow([new Date(), dados.nome, dados.email]);
     return ContentService.createTextOutput("Sucesso");
   }

   function doGet() {
     const aba = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
     const [cabecalho, ...linhas] = aba.getDataRange().getValues();
     const lista = linhas.map(l =>
       Object.fromEntries(cabecalho.map((c, i) => [c, l[i]]))
     );
     return ContentService
       .createTextOutput(JSON.stringify(lista))
       .setMimeType(ContentService.MimeType.JSON);
   }
   ```

3. Clique em **Implantar → Nova implantação → Aplicativo da Web** e libere o acesso.
4. Copie a URL gerada (termina em `/exec`).
5. No notebook, troque o valor de `API_URL` pela sua URL e execute as células.

### 🔒 Atenção com a URL

A URL do Apps Script funciona como uma "chave": **quem tiver o link consegue gravar na sua planilha**. Use a sua própria e não a publique em repositórios públicos.

---

## 🧠 Conceitos praticados

- O que é uma **API** e como ela troca dados com o código
- Requisições HTTP com `requests`: **GET** (ler) e **POST** (enviar)
- Dados em formato **JSON** (objetos e listas)
- Parâmetros de URL (`/random/N` e `?limit=N`)
- Funções, laços com `enumerate` e listas de dicionários
- Manipulação de arquivos e pastas com `os`
- Geração de HTML e arquivos `.zip` com Python
- Integração entre Python, Google Sheets e Apps Script

## 🔜 Próximos passos

- [ ] Adicionar as próximas aulas do bootcamp
- [ ] Praticar com outras APIs públicas
- [ ] Análise de dados com Python (pandas)

## 👤 Autor

**Thúlio Ferreira Jacauna**
Estudante de Gestão em TI e do bootcamp de Análise de Dados (Generation Brasil).

- GitHub: [@Thuliofj](https://github.com/Thuliofj)
- X: [@ThulioFJ](https://x.com/ThulioFJ)
