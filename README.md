# Documentação do Projeto: Base de Dados SPARQL para Games 🎮

## Objetivo do Projeto

- O objetivo deste projeto é criar uma base de dados semântica para armazenar informações sobre jogos eletrônicos, utilizando o formato RDF (Resource Description Framework). Essa base de dados permite consultas poderosas e flexíveis via SPARQL, possibilitando a exploração e análise de informações detalhadas sobre jogos, como desenvolvedores, plataformas, anos de lançamento, e muito mais.

---

## O Que é RDF?

RDF é um modelo padrão para intercâmbio de dados na web semântica. Ele organiza as informações em triplas no formato:

**Sujeito – Predicado – Objeto**

  Por exemplo:

- **Minecraft** – foi_desenvolvido_por – **Mojang**

  Este formato facilita o armazenamento e recuperação de dados relacionados, permitindo a integração de informações de diversas fontes.

---

## O Que é SPARQL?

SPARQL é uma linguagem de consulta projetada para buscar e manipular dados armazenados em formato RDF. Ele permite a realização de buscas precisas, incluindo filtros avançados, agrupamentos e ordenações, ideal para análises complexas.

---

## Funcionalidades do Projeto

- **Armazenar Dados de Games:** Informações como nome, desenvolvedor, ano de lançamento e plataformas.
- **Consultas SPARQL:** Permite acessar e explorar os dados com consultas personalizadas.
- **Visualização e Análise:** Dados podem ser exportados e analisados com ferramentas como Python.

---

## Estrutura dos Dados

Os dados são representados por uma ontologia RDF simplificada. Aqui estão os principais elementos:

### Classes:
- **Game:** Representa um jogo eletrônico.

### Propriedades:
- `ex:nome_`: Nome do jogo.
- `ex:desenvolvedor_`: Empresa ou pessoa que desenvolveu o jogo.
- `ex:lancamento_`: Ano de lançamento.
- `ex:plataformas_`: Plataformas onde o jogo está disponível.

**Exemplo de tripla:**
- Minecraft – `ex:nome_` – "Minecraft"
- Minecraft – `ex:desenvolvedor_` – "Mojang"
- Minecraft – `ex:lancamento_` – "2011"

---

## Tecnologias Utilizadas

- **Virtuoso:** Servidor RDF para armazenar e consultar os dados.
- **Python:** Linguagem de programação para manipulação de dados e integração.

### Bibliotecas:
- **rdflib:** Gera e manipula arquivos RDF.
- **rdflib_neo4j:** Integração com bases gráficas como Neo4j.
- **pandas:** Manipulação de dados tabulares.
- **matplotlib:** Visualização gráfica dos dados.

---

## Passo a Passo: Implementação

### 1. Preparação do Ambiente

O ambiente virtual é configurado com bibliotecas essenciais para lidar com arquivos RDF, consultas SPARQL e visualização de dados.

### 2. Criação do Arquivo RDF

Um arquivo RDF é gerado em Python, contendo informações dos jogos. Cada jogo é representado como um conjunto de triplas.

### 3. Importação para Virtuoso

Os dados RDF são importados para o Virtuoso, que permite a execução de consultas SPARQL diretamente na base.

### 4. Execução de Consultas SPARQL

Exemplos de consultas são executados para extrair informações como:

- Lista de jogos lançados após um ano específico.
- Jogos de um determinado desenvolvedor.
- Contagem de jogos por desenvolvedor.



## Exemplos de Consultas

### Selecionar Todos os Jogos

Esta consulta retorna todos os jogos na base, com informações como nome, desenvolvedor, ano de lançamento e plataformas:

```sparql
PREFIX ex: <http://example.org/games/>

SELECT ?nome_ ?desenvolvedor_ ?lancamento_ ?plataformas_
WHERE {
  ?game ex:nome_ ?nome_ ;
        ex:desenvolvedor_ ?desenvolvedor_ ;
        ex:lancamento_ ?lancamento_ ;
        ex:plataformas_ ?plataformas_ .
}
LIMIT 100
```

---

### Filtrar Jogos por Desenvolvedor

Exemplo para listar jogos desenvolvidos pela Mojang:

```sparql
PREFIX ex: <http://example.org/games/>

SELECT ?nome ?ano
WHERE {
  ?game ex:nome_ ?nome ;
        ex:desenvolvedor_ ?desenvolvedor ;
        ex:lancamento_ ?ano .
  FILTER (str(?desenvolvedor) = "Mojang")
}
LIMIT 100
```

---
### Potenciais Aplicações

- Análise de Tendências: Estudo de padrões de lançamentos, popularidade de plataformas e desenvolvedores.
- Pesquisa Acadêmica: Exploração de dados relacionados ao mercado de jogos.
- Integração com Outras Bases: Enriquecimento da base RDF com dados adicionais de APIs públicas.


Com este projeto, é possível explorar o mundo dos games de forma semântica e conectada, abrindo portas para análises mais profundas e detalhadas. 🚀

---

# Guia de Configuração e Consultas SPARQL para Base de Games

## Criar o Ambiente Virtual

Para criar e ativar um ambiente virtual em Python, execute o comando abaixo:

```bash
python3 -m venv games
```

## Ativar o Ambiente Virtual

Ative o ambiente virtual com o comando:

```bash
source games/bin/activate
```

## Listar as Bibliotecas Instaladas

Para ver as bibliotecas instaladas no ambiente, use:

```bash
pip list
```

## Desativar o Ambiente Virtual

Para desativar o ambiente, execute:

```bash
deactivate
```

## Instalar as Bibliotecas Necessárias

Instale as bibliotecas necessárias para o projeto com:

```bash
pip install pandas openpyxl matplotlib rdflib rdflib_neo4j
```

## Gerar `requirements.txt`

Para gerar um arquivo `requirements.txt` contendo todas as dependências instaladas no ambiente virtual, use:

```bash
pip freeze > requirements.txt
```

## Instalar Pacotes do `requirements.txt`

Caso você precise instalar os pacotes listados em `requirements.txt`, execute:

```bash
pip install -r requirements.txt
```

## Configuração do Banco de Dados Virtuoso

### Conectar ao Virtuoso

Acesse o **Virtuoso** para importar dados:

- **URL:** [Virtuoso](http://200.129.247.238:8890/conductor/)
- **Usuário:** `dba`
- **Senha:** `dba`

## Importar o Arquivo RDF `base_games.rdf`

1. No Virtuoso, acesse a seção de **Quad Store Upload**.
2. Faça o upload do arquivo `base_games.rdf` gerado no Python.
3. Acesse a seção **SPARQL** para realizar consultas na base de dados.


## Consultas SPARQL

### 1. Consultar Todos os Games

```sparql
PREFIX ex: <http://example.org/games/>

SELECT ?nome_ ?desenvolvedor_ ?lancamento_ ?plataformas_
WHERE {
  ?game ex:nome_ ?nome_ ;
        ex:desenvolvedor_ ?desenvolvedor_ ;
        ex:lancamento_ ?lancamento_ ;
        ex:plataformas_ ?plataformas_ .
}
LIMIT 100
```

### 2. Selecionar jogos lançados após 2000

Para filtrar jogos que estão disponíveis em uma plataforma específica, como "PC":

```sparql
PREFIX ex: <http://example.org/games/>

SELECT ?nome ?desenvolvedor ?ano
WHERE {
  ?game ex:nome_ ?nome ;
        ex:desenvolvedor_ ?desenvolvedor ;
        ex:lancamento_ ?ano .
  FILTER (xsd:int(?ano) > 2000)
}
LIMIT 100
```

### 3. Selecionar jogos de um determinado desenvolvedor

```sparql
PREFIX ex: <http://example.org/games/>

SELECT ?nome ?ano
WHERE {
  ?game ex:nome_ ?nome ;
        ex:desenvolvedor_ ?desenvolvedor ;
        ex:lancamento_ ?ano .
  FILTER (str(?desenvolvedor) = "Mojang")
}
LIMIT 100
```

### 4. Selecionar jogos com "Saga" no nome

Para listar jogos filtrando por gênero, como "Ação":

```sparql
PREFIX ex: <http://example.org/games/>

SELECT ?nome ?desenvolvedor ?ano
WHERE {
  ?game ex:nome_ ?nome ;
        ex:desenvolvedor_ ?desenvolvedor ;
        ex:lancamento_ ?ano .
  FILTER (CONTAINS(str(?nome), "Saga"))
}
LIMIT 100
```

### 5.  Selecionar o número de jogos por desenvolvedor

Para listar os jogos lançados em 2020:

```sparql
PREFIX ex: <http://example.org/games/>

SELECT ?desenvolvedor (COUNT(?game) AS ?quantidade_de_jogos)
WHERE {
  ?game ex:desenvolvedor_ ?desenvolvedor ;
        ex:nome_ ?nome .
}
GROUP BY ?desenvolvedor
ORDER BY DESC(?quantidade_de_jogos)
LIMIT 100
```
