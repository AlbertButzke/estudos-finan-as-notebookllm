# 📊 Miniguia de Estudos: Gestão de Risco de Crédito e Mercado com NotebookLM

[![GitHub](https://img.shields.io/badge/GitHub-Repository-181717?style=flat-square&logo=github)](https://github.com/AlbertButzke/estudos-finan-as-notebookllm)
[![Google NotebookLM](https://img.shields.io/badge/Google-NotebookLM-4285F4?style=flat-square&logo=google)](https://notebooklm.google.com/notebook/d76c1fba-1779-4409-b5d2-b828e9978da2)
[![DIO](https://img.shields.io/badge/DIO-Desafio%20de%20Projeto-A31D1D?style=flat-square)](https://web.dio.me/users/felipe_a_butzke)

Este repositório foi desenvolvido como parte de um desafio prático da **DIO (Digital Innovation One)**. O objetivo principal é utilizar o **Google NotebookLM** como uma ferramenta de aprendizagem ativa para explorar, estruturar e consolidar conceitos fundamentais de gestão de risco de crédito e mercado em instituições financeiras.

---

## 1. Contexto e Objetivos

O intuito deste estudo é compreender a fundo como os bancos mitigam riscos, calculam a saúde de suas carteiras e se protegem contra calotes. 

Utilizando o poder de síntese e cruzamento de fontes do NotebookLM, o foco foi mapear e dominar as seguintes métricas iniciais de finanças quantitativas e risco:
* **PD** (*Probability of Default* / Probabilidade de Inadimplência)
* **LGD** (*Loss Given Default* / Perda Dada a Inadimplência)
* **EAD** (*Exposure at Default* / Exposição na Inadimplência)
* **VaR** (*Value at Risk* / Valor em Risco)
* **NPL Ratio** (Taxa de Inadimplência / *Non-Performing Loans*)

---

## 2. Curadoria de Fontes

Para alimentar a base de conhecimento do NotebookLM, foram selecionados de 3 a 5 artigos, glossários e papers técnicos de referência no mercado financeiro global:

* 📖 [Quantitative Risk Management - Chapter 5 (IAM FMPH)](http://www.iam.fmph.uniba.sk/institute/jurca/qrm/Chapter5.pdf)
* 🔗 [Glossário de Risco de Crédito - StoneX](https://www.stonex.com/pt-br/empresas/glossario-financeiro/risco-de-credito/)
* 🧠 [Expected Loss: Definition, Calculation & Importance - CFI](https://corporatefinanceinstitute.com/resources/career-map/sell-side/risk-management/expected-loss-definition-calculation-importance/)
* 📈 [Understanding EAD, LGD and PD - LearnSignal](https://www.learnsignal.com/blog/exposure-at-default-loss-given-default-and-probability-of-default/)
* 🏦 [How is a bank's credit quality measured? - BBVA](https://www.bbva.com/en/economy-and-finance/how-is-a-banks-credit-quality-measured/)
* 📝 [Deep Dive into Probability of Default - Abrigo](https://www.abrigo.com/blog/blog-probability-of-default/)

---

## 3. Engenharia de Prompts e "Cicatrizes"

### O Prompt de Partida (Contextualização)
Para extrair o melhor nível de resposta da IA, adotei uma abordagem de **persona reversa**, explicando meu background exato (Mestre em Cosmologia com forte base matemática/estatística), permitindo que a IA pulasse explicações rasas e fosse direto à modelagem matemática:

> "Sou iniciante nos estudos de mercado financeiro, bancos e economia, no entanto possuo uma base forte de matemática, estatística e física, pois sou mestre em cosmologia, então acredito que entendo os conceitos base para os cálculos e conceitos avançados.
> 
> Portanto, gostaria de entender, com base nisso, os cálculos de Probability of Default (PD), Loss Given Default (LGD), Exposure at Default (EAD) e taxa de inadimplência. Além de entender os cálculos, quero saber o que é cada uma dessas variáveis e como podem ser usados pelo banco e instituições financeiras."

### 🧠 O Retorno Técnico da IA (Consolidado)

Para um perfil analítico, o risco de crédito é modelado como um conjunto de **eventos estocásticos**. Abaixo estão os pilares extraídos e revisados para o contexto bancário brasileiro:

#### 1. Exposure at Default (EAD) — Exposição no Momento da Inadimplência
Representa o saldo devedor total que o cliente possui com o banco no exato momento do *default*.
* **Dinâmica:** Em empréstimos de parcelas fixas (*Term Loans*), a EAD decresce no tempo. Em linhas de crédito rotativas (como cartão de crédito), a EAD soma o saldo utilizado atual com uma projeção do limite que o cliente ainda pode sacar antes de quebrar, calculada via CCF (*Credit Conversion Factor*).
* **Uso Bancário:** Dimensionamento de testes de estresse (*stress testing*) e limites de concentração de carteira.

#### 2. Probability of Default (PD) — Probabilidade de Inadimplência
Mede a chance de um tomador de crédito entrar em default em um horizonte de tempo (geralmente 12 meses). Pode ser abordada por duas grandes óticas matemáticas:
* **Modelos Estruturais (ex: Modelo de Merton):** Baseado em cálculo estocástico, onde o valor dos ativos da empresa ($A_t$) segue um Movimento Browniano Geométrico:
  $$dA_t = \mu_A A_t dt + \sigma_A A_t dW_t$$
  O *default* ocorre se, no vencimento, o valor do ativo for menor que a dívida ($D_t$).
* **Modelos de Forma Reduzida (Macroeconométricos):** Utilizam variáveis macroeconômicas mapeadas através de uma regressão logística (*transformação logit*) para garantir que a PD fique estritamente entre 0 e 1:
  $$PD_t = \frac{1}{1 + e^{-y_t}}$$
  Onde $y_t$ é uma combinação linear de fatores como variação do PIB, desemprego e inflação.

#### 3. Loss Given Default (LGD) — Perda Dada a Inadimplência
É a perda real (em percentual) sofrida pela instituição após o esgotamento das tentativas de recuperação de crédito (cobrança/judicial).
* **Cálculo:** Ligado diretamente à Taxa de Recuperação (*Recovery Rate* ou $RR$):
  $$LGD = 1 - RR$$
* **Uso Bancário:** Determina a necessidade e a qualidade de garantias (colaterais) exigidas na estruturação de novas operações.

#### 4. Taxa de Inadimplência (NPL Ratio)
O *Non-Performing Loans Ratio* mede a saúde geral e a qualidade do estoque da carteira de crédito da instituição.
* **Cálculo:**
  $$NPL\ Ratio = \left( \frac{\text{Empréstimos Inadimplentes (Atraso } \ge \text{ 90 dias)}}{\text{Total da Carteira de Crédito}} \right) \times 100$$
* **Uso Bancário:** Indicador crucial para o mercado, reguladores (Banco Central) e acionistas. Uma alta no NPL exige o aumento imediato de Provisões (PECL - Perda Estimada em Crédito de Liquidação Duvidosa), impactando diretamente o lucro líquido.

### 📐 A Integração dos Conceitos: Perda Esperada vs. Inesperada
A união dessas três variáveis gera a métrica regulatória de **Perda Esperada (Expected Loss - EL)**:

$$EL = PD \times LGD \times EAD$$

> ⚠️ **Nota de Troubleshooting / Cicatrizes de Aprendizado:** 
> Durante as interações com a IA, notei que algumas fórmulas matemáticas ocultavam subindexações importantes e misturavam termos da tradução literal em inglês com a contabilidade bancária brasileira (ex: traduzir *provisions* apenas como "provisões gerais" em vez de associar ao conceito contábil e regulatório de PDD/PECL e às regras de Basileia III). Foi necessário ajustar os prompts seguintes para trazer os conceitos para o escopo do ecossistema financeiro nacional.

---

## 4. Miniguia de Estudo (Entrega Final)

### 📝 Resumo Executivo
Instituições financeiras operam gerenciando incertezas. A precisão no cálculo de métricas como PD, LGD e EAD separa bancos insolventes de bancos resilientes. Enquanto a **Perda Esperada (EL)** é precificada diretamente nos juros cobrados e absorvida pelas provisões contábeis diárias, volatilidades extremas e eventos de cauda (como crises sistêmicas) configuram a **Perda Inesperada (UL)**, combatida através do colchão de Capital Próprio exigido pelos acordos internacionais de Basileia.

### 📖 Glossário Técnico

| Termo | Significado no Mercado |
| :--- | :--- |
| **Default** | Inadimplência formal; descumprimento de cláusulas contratuais de pagamento por período determinado (usualmente $\ge$ 90 dias). |
| **Recovery Rate (RR)** | Taxa de Recuperação. Percentual da dívida que o banco consegue reaver através de garantias, leilões ou renegociações. |
| **Mitigação de Risco** | Uso de mecanismos (como colaterais, avais ou derivativos) para reduzir a LGD ou a EAD de uma operação. |
| **Basileia III** | Acordo regulatório global que impõe limites mínimos de capital regulatório ponderado pelo risco (RWA) para garantir liquidez aos bancos. |

### 🛠️ Prompts Reutilizáveis para Estudos Futuros

Copie e cole estes prompts no seu NotebookLM ou LLM de preferência para continuar explorando o tema:

#### 1. Contextualização Avançada (Foco Quantitativo)
```text
[Fale aqui a sua base de conhecimento sobre matemática e estatística.]

[Fale que quer aprender sobre as métricas e proteções dos bancos, como: Probability od Default (PD), Loss Given Default (LGD), Exposure at Default (EAD) e taxa de inadimplência].

[Fale que gostaria de entender como essas métricas são usadas pelos bancos e instituições financeiras.]
```

#### 2. Criação de Mapas Mentais Operacionais
```text
Gere uma estrutura de mapa mental conectando os principais pilares de gerenciamento de risco de crédito bancário. O mapa deve ramificar a partir de: 1) Métricas Base (PD, LGD, EAD, NPL) com suas respectivas equações; 2) Ferramentas de Proteção (Provisões vs Capital Regulatório); e 3) Aplicação Prática (Pricing de Crédito). Utilize o português brasileiro, mas preserve as siglas internacionais entre parênteses.
```
#### 3. Roteirização de Apresentação Executiva
```text
Crie o roteiro de uma apresentação de slides explicando a jornada da gestão de risco bancário como uma defesa contra incertezas. Inclua na estrutura explicações conceituais, analogias práticas e as formulações matemáticas das seguintes siglas: EL, UL, PD, LGD, EAD, RR, NPL Ratio, RWA, Coverage Ratio e Cost of Risk. Finalize explicando como choques macroeconômicos alteram estes parâmetros dinamicamente.
```

Caderno temático criado com orgulho para o Portfólio de Data Science & Finanças. 🚀
