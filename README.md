# 🌐 Dados de Sites — Coleta de Dados Online com Web Scraping

> Projeto desenvolvido durante o **Sprint 6** do bootcamp [TripleTen](https://tripleten.com/), com foco em **extração automatizada de dados da web** utilizando as bibliotecas `requests` e `BeautifulSoup`, transformando páginas HTML em dados estruturados e prontos para análise.

---

## 📌 Sobre o Projeto

Este projeto demonstra como coletar dados diretamente de páginas da internet de forma automatizada — uma habilidade essencial para analistas de dados que precisam trabalhar com fontes de dados que não oferecem arquivos para download.

Utilizando **web scraping**, o notebook acessa páginas HTML, identifica os elementos de interesse com **BeautifulSoup**, extrai as informações relevantes e as organiza em um **DataFrame Pandas** para análise posterior.

---

## 🎯 Objetivos

- Realizar requisições HTTP a páginas web com a biblioteca `requests`
- Analisar a estrutura HTML de uma página para identificar os dados-alvo
- Extrair informações estruturadas com **BeautifulSoup**
- Organizar os dados coletados em um DataFrame com **Pandas**
- Tratar e limpar os dados extraídos para uso analítico
- Armazenar os dados coletados para análises futuras

---

## 🗂️ Estrutura do Repositório

```
📁 Dados-de-Sites/
│
├── 📓 Pegando_dados_sites.ipynb   # Notebook principal com o processo de scraping
└── 📄 README.md                   # Documentação do projeto
```

---

## 🔍 Etapas do Processo

### 1. Entendendo a Estrutura da Página
- Inspeção do HTML da página-alvo via DevTools do navegador
- Identificação das tags, classes e atributos que contêm os dados de interesse
- Mapeamento da estrutura de navegação (paginação, links, hierarquia)

### 2. Fazendo Requisições com `requests`
- Envio de requisições `GET` para a URL da página
- Verificação do status da resposta (`status_code`)
- Configuração de headers para simular um navegador real
- Tratamento de erros de conexão e respostas inesperadas

### 3. Parsing do HTML com `BeautifulSoup`
- Parsing do conteúdo HTML com `BeautifulSoup(html, 'html.parser')`
- Localização de elementos com `.find()` e `.find_all()`
- Extração de texto com `.get_text()` e atributos com `.get()`
- Navegação pela árvore DOM (parent, children, siblings)
- Uso de seletores CSS com `.select()` e `.select_one()`

### 4. Coleta e Estruturação dos Dados
- Iteração sobre múltiplos elementos da página
- Raspagem de múltiplas páginas com controle de paginação
- Organização dos dados coletados em listas e dicionários
- Criação de um `DataFrame` Pandas a partir dos dados extraídos

### 5. Limpeza e Tratamento dos Dados
- Remoção de espaços extras e caracteres especiais com `.strip()`
- Conversão de tipos de dados (preços, datas, números)
- Tratamento de valores ausentes nos dados coletados
- Padronização de formatos para garantir consistência

### 6. Análise e Exportação
- Inspeção e validação dos dados coletados
- Análise exploratória básica sobre os dados extraídos
- Exportação do DataFrame para `.csv` para uso futuro

---

## 🛠️ Tecnologias Utilizadas

| Ferramenta | Finalidade |
|---|---|
| Python 3 | Linguagem principal |
| `requests` | Requisições HTTP para acessar páginas web |
| `BeautifulSoup4` | Parsing e extração de dados do HTML |
| `lxml` / `html.parser` | Parser de HTML/XML |
| Pandas | Organização e manipulação dos dados coletados |
| Jupyter Notebook | Ambiente de desenvolvimento interativo |

---

## 💻 Exemplo do Fluxo de Scraping

```python
import requests
from bs4 import BeautifulSoup
import pandas as pd

# 1. Requisição à página
url = 'https://exemplo.com/dados'
headers = {'User-Agent': 'Mozilla/5.0'}
response = requests.get(url, headers=headers)

# 2. Parsing do HTML
soup = BeautifulSoup(response.text, 'html.parser')

# 3. Extração dos dados
itens = soup.find_all('div', class_='item')
dados = []

for item in itens:
    nome  = item.find('h2').get_text(strip=True)
    preco = item.find('span', class_='preco').get_text(strip=True)
    dados.append({'nome': nome, 'preco': preco})

# 4. Criação do DataFrame
df = pd.DataFrame(dados)
df['preco'] = df['preco'].str.replace('R$', '').str.strip().astype(float)
```

---

## ▶️ Como Executar

1. Clone o repositório:
```bash
git clone https://github.com/caguiar0/Dados-de-Sites.git
```

2. Acesse a pasta do projeto:
```bash
cd Dados-de-Sites
```

3. Instale as dependências:
```bash
pip install requests beautifulsoup4 lxml pandas jupyter
```

4. Inicie o Jupyter Notebook:
```bash
jupyter notebook
```

5. Abra o arquivo `Pegando_dados_sites.ipynb` e execute as células sequencialmente.

> ⚠️ **Atenção:** A disponibilidade dos dados depende do site-alvo estar acessível no momento da execução. Caso o site tenha alterado sua estrutura HTML desde a criação do notebook, pode ser necessário ajustar os seletores.

---

## 📋 Métodos BeautifulSoup Cobertos

| Método | Descrição |
|---|---|
| `find(tag, attrs)` | Localiza o primeiro elemento que corresponde ao critério |
| `find_all(tag, attrs)` | Retorna todos os elementos que correspondem ao critério |
| `select(css_selector)` | Seleciona elementos por seletor CSS |
| `get_text(strip=True)` | Extrai o texto limpo do elemento |
| `.get('atributo')` | Obtém o valor de um atributo HTML (ex: `href`, `src`) |
| `.parent` / `.children` | Navega para elementos pai ou filhos |
| `.next_sibling` | Acessa o próximo elemento irmão na árvore HTML |

---

## ⚖️ Boas Práticas de Web Scraping

- ✅ Verificar o arquivo `robots.txt` do site antes de raspar
- ✅ Respeitar intervalos entre requisições para não sobrecarregar o servidor
- ✅ Usar `headers` para identificar corretamente a requisição
- ✅ Tratar exceções (`try/except`) para lidar com falhas de conexão
- ✅ Armazenar os dados coletados localmente para evitar raspagens repetidas

---

## 💡 Insights Obtidos

> ⚠️ *Preencha esta seção com os dados coletados e insights extraídos no seu notebook, como:*
> - Qual site foi usado como fonte dos dados
> - Quais informações foram extraídas (preços, títulos, datas, etc.)
> - Principais padrões ou descobertas nos dados coletados

---

## 🏅 Habilidades Demonstradas

- ✅ Coleta automatizada de dados com `requests` e `BeautifulSoup`
- ✅ Navegação e parsing de estruturas HTML complexas
- ✅ Transformação de dados não estruturados (HTML) em dados tabulares
- ✅ Limpeza e tratamento de dados coletados da web
- ✅ Boas práticas de ética e eficiência em web scraping

---

## 👤 Autor

**caguiar0**  
Projeto desenvolvido como parte do currículo de Análise de Dados da [TripleTen](https://tripleten.com/).

---

## 📄 Licença

Este projeto é de uso educacional e está disponível para fins de estudo e portfólio.
