# 🏛️ A Impressão Digital do Parlamentar: Uma Anatomia Multidimensional da Atuação Legislativa

## Visão geral do projeto
Este repositório contém o projeto prático desenvolvido para a disciplina de Introdução à Ciência de Dados. O foco central da pesquisa é investigar e traduzir o complexo volume de dados públicos do poder legislativo em uma "impressão digital" clara, quantificável e compreensível de cada parlamentar.

---

## 🎯 Objetivos

### Objetivo Principal:
> Mapear e analisar o comportamento legislativo dos parlamentares por meio de dados abertos, construindo uma "impressão digital" baseada em evidências que revele padrões de atuação, prioridades temáticas, alinhamentos políticos e o uso de recursos públicos.

### Objetivos Específicos

 >  **Consolidação de Dados:** Integrar e higienizar bases de dados heterogêneas em um formato tabular estruturado e confiável.

 >  **Análise de Eficiência e Gastos:** Identificar possíveis correlações entre os gastos de gabinete e o volume/relevância das atividades legislativas propostas.

 > **Visualização de Padrões:** Desenvolver visualizações gráficas que facilitem a interpretação de dados complexos, tornando o perfil do parlamentar acessível a qualquer cidadão.

---

## ✍🏻 Descrição do Conjuto de Dados

O presente conjunto de dados foi construído a partir da coleta de informações por meio da API pública de despesas dos deputados. A partir dessa fonte, foi possível obter um volume significativo de dados, permitindo a extração de informações relevantes para diversas análises. A diversidade de atributos e a confiabilidade das informações, por serem provenientes de uma base oficial, tornam o dataset um campo fértil para exploração. O conjunto inclui um arquivo CSV com registros detalhados das despesas parlamentares, possibilitando a identificação de padrões de gastos e a realização de análises históricas ao longo do tempo.

Além disso, o dataset contempla variáveis importantes, como filiação partidária, categorias de gastos, recorrência de mandatos, nível de escolaridade e sexo dos parlamentares, entre outras características relevantes. Essa riqueza de informações contribui para análises mais robustas e aprofundadas. Apesar dos desafios associados ao tratamento e à manipulação de grandes volumes de dados, a abrangência e a qualidade do conjunto proporcionam maior confiabilidade aos resultados, tornando-o adequado para a construção de análises consistentes e detalhadas no contexto deste projeto.

---

## 🎲 Processo de Coleta de Dados

Para realizar a coleta de dados, foi utilizada a API de dados abertos da Câmara dos Deputados. A partir dessa API, dividimos as informações coletadas na criação de três *datasets* diferentes:

### 1. Dataset de Deputados
* Tivemos que varrer os dados duas vezes durante a coleta.
* **Primeira etapa:** Foi feita para coletar todos os deputados. Como cada requisição trazia 100 resultados por vez, precisamos navegar pelas páginas e pelos anos para obter a lista completa.
* **Segunda etapa:** Acessamos os dados de um por um através do ID. O objetivo era pegar informações mais detalhadas sobre eles, como a data de nascimento, se o deputado já faleceu e o estado em que nasceu.

### 2. Dataset de Despesas
* **Requisições individuais:** Tivemos que fazer requisições individuais para cada deputado (de uma a cinco requisições por parlamentar), pois a API não permite coletar as despesas gerais, apenas listando por deputado.
* **Navegação:** Assim como no primeiro *dataset*, a coleta trazia os dados de 100 em 100, o que exigiu que navegássemos entre as páginas de despesas de cada deputado.
* **Ajuste manual:** Tivemos também o trabalho de acessar e adicionar uma coluna extra com o ID do deputado, pois as despesas naturalmente não vinham com o ID vinculado a elas.

### 3. Dataset de Proposições
* **Tempo de coleta:** Este foi o *dataset* que mais demorou para ser coletado, levando cerca de 4 horas rodando.
* **Abrangência:** Tivemos que navegar por todas as proposições desde o ano de 2000, coletando ano a ano até 2025, o que envolveu muitas páginas a cada ano.
* **Obs.:** Apesar da coleta ter sido feita, nós não vamos utilizar esse *dataset* de proposições na nossa análise de dados. O nosso foco principal será em analisar o *dataset* de despesas.

---

## 📄 Documentação
``` bash
https://drive.google.com/drive/folders/1459TTvARra90e6lcWu53kMy9Np4Ix0nT?usp=drive_link
```

---


## 📁 Estruturação do Dataset

Os arquivos do dataset são arquivos CSV contendo dados de indentificação sobre os deputados. 

### Formato dos Dados:

|  id  |       uri        | nomeParlamentar |     siglaPartido   |    uriPartido    |  siglaUf | idLegislatura  |    urlFoto     | email | sexo | ultimaSituacao | condicaoEleitoral | nomeEleitoral  |      nomeCivil    | dataNascimento | falecido | ufNascimento | escolaridade |
|------|------------------|-----------------|--------------------|------------------|----------|----------------|----------------|-------|------|-----------|---------|----------------|-------------------|----------------------|----------|--------------|--------------|
| 1500 | https://dados... | MÁRIO LIMA | "['PMDB', 'PSB*']" | https://dados... |  ['BA']  | "[48, 42, 47]" |     https://www...     | |   M  | Vacância  | Titular |   MÁRIO LIMA   | MÁRIO SOARES LIMA |   1935-02-19   |     0    |      BA      |   Secundário |
| 1501 | https://dados... |  MAURÍCIO FRUET  |"['PMDB', 'MDB*']" |https://dados...  |  ['PR']  | "[48, 46, 47]" |     https://www...     | |   M  |  Vacância | Titular | MAURÍCIO FRUET | Maurício Roslindo Fruet | 1939-08-12 | 0 | PR | Superior |

---

### Descrição Colunas:

| Coluna | Descrição |
|---|-------|
| `id` | Identificador único do parlamentar no sistema da Câmara dos Deputados. |
| `uri` | Endereço de acesso (URL) aos dados completos do parlamentar diretamente na API. |
| ``nomeParlamentar``  | Nome público pelo qual o político atua e é conhecido na Câmara.  |
| `siglaPartido` | Histórico das siglas partidárias às quais o parlamentar esteve filiado ao longo das legislaturas registradas. | 
| `uriPartido` | Endereço de acesso (URL) aos dados do partido associado. |
| `siglaUf `| Histórico das Unidades da Federação (estados) pelas quais o parlamentar foi eleito. |
| ``idLegislatura`` | Identificadores numéricos correspondentes aos períodos de legislatura (mandatos de 4 anos) em que o parlamentar esteve ativo. | 
| ``urlFoto`` | Link de acesso direto para o retrato oficial do parlamentar. | 
| ``email`` | Link de acesso direto para o retrato oficial do parlamentar. | 
| ``sexo`` | Sexo do parlamentar ( ``M`` para Masculino, ``F`` para Feminino). | 
| ``ultimaSituação`` | Último status registado do mandato do parlamentar. |
| ``condicaoEleitoral`` | Condição na qual o parlamentar assumiu o mandato. |
| ``nomeEleitoral`` | Nome utilizado pelo candidato nas urnas e em campanhas eleitorais. |
| ``nomeCivil`` | Nome completo de registo civil do indivíduo. |
| ``dataNascimento`` | Data de nascimento formatada no padrão ISO |
| ``falecido`` | Indicador binário sobre o óbito do parlamentar( ``0`` para vivo e ``1`` para falecido). |
| ``ufNascimento`` | Sigla da Unidade da Federação de naturalidade do parlamentar. |
| ``escolaridade`` | Grau máximo de instrução formal declarado. |

---

