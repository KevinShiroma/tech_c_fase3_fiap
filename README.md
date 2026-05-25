# Tech Challenge - Fase 2: Otimização Genética e Interpretação de Diagnósticos com LLM

Este repositório contém o projeto da **Fase 2** do Tech Challenge (Pós-Tech IA para Devs). O projeto evolui a base do sistema de suporte ao diagnóstico da Fase 1, incorporando **Algoritmos Genéticos (AG)** para a otimização de hiperparâmetros e **Modelos de Linguagem de Grande Escala (LLM)** para a interpretação humanizada dos resultados médicos.

## 📺 Demonstração do Projeto
* **Link para o YouTube:** https://www.youtube.com/watch?v=5YBZP57DvKs
* **Apresentação:** Demonstração do pipeline no Databricks, tracking no MLflow e geração de insights via GPT-4o.

## 🛠️ Arquitetura do projeto

<img width="2944" height="1248" alt="image" src="https://github.com/KevinShiroma/tech_c_fase2_fiap/blob/main/arquitetura/arquitetura_projeto.png" />

O projeto foi desenvolvido em ambiente Databricks, utilizando a Arquitetura Medalhão (Delta Lake) para garantir a governança dos dados médicos.

* **Processamento & Escalabilidade:** Clusters Spark com Autoscaling para lidar com o processamento paralelo das populações do AG e grandes volumes de dados.

* **Observabilidade:** MLflow Tracking para monitoramento de métricas (F1-Score), parâmetros e versões dos modelos otimizados.

* **IA Generativa:** OpenAI GPT-4o para a camada de interpretação em linguagem natural.

## 📋 Sobre a Evolução (Fase 2)

O foco desta etapa foi elevar a precisão clínica e a interpretabilidade do sistema hospitalar através de duas frentes tecnológicas principais:

### 1. Otimização Evolutiva (Algoritmos Genéticos)
Substituímos a busca manual de parâmetros por um processo de evolução artificial para os modelos KNN e Random Forest:
* **Codificação Genética:** Os hiperparâmetros (como n_estimators, max_depth e k-neighbors) foram mapeados como genes.
* **Operadores Genéticos:** Implementação de seleção por roleta russa, cruzamento aritmético e mutação aleatória.
* **Função Fitness:** Otimização baseada no **F1-Score da Classe 0 (Risco)**, garantindo uma triagem médica rigorosa em dados desbalanceados.

### 2. Interpretação de Resultados (LLM & Prompt Engineering)
Integração com a API da OpenAI (GPT-4o) para transformar predições técnicas em relatórios clínicos acionáveis:
* **Persona:** Atuação da LLM como "Assistente de Diagnóstico Psiquiátrico".
* **Top 5 Indicadores:** O prompt utiliza as variáveis de maior importância identificadas pelo Random Forest (anxiety_score, depression_score, productivity_score, social_support_score e sleep_hours).
* **Insights Acionáveis:** Geração automática de recomendações de conduta imediata (ex: higiene do sono, busca por terapia) para a equipe médica.

---

## 📂 Estrutura do Projeto

```text
/
├── .env                           # chaves de API da OpenAI, coloque a variável CHAT_GPT_KEY = <SEU_TOKEN>
├── note_create_raw                # Ingestão de dados brutos (Camada Bronze)
├── note_cleaning_transform_silver # Limpeza e padronização (Camada Silver)
├── note_create_gold               # Engenharia de features (Camada Gold)
├── note_predict_doenca_original   # Modelos base desenvolvidos da fase 1 para comparação
└── note_predict_doenca_alg_gen    # Pipeline principal: AG + Otimização + LLM (Fase 2)
```

## 🚀 Guia de Execução

Pré-requisitos
* Conta no Databricks Free Edition - [Login page - Databricks](https://login.databricks.com/signup?intent=SIGN_UP&provider=DB_FREE_TIER)
* Chave de API da OpenAI. - [OpenAI - Developers](https://platform.openai.com/home)

Passo 1: Configuração do Ambiente
Configure o arquivo .env com a sua credencial:

```bash

CHAT_GPT_KEY = <SEU_TOKEN>

```

Passo 2: Execução do Notebook
Execute os notebooks de processamento (raw -> silver -> gold) para preparar os dados.

Utilize o notebook note_predict_doenca_alg_gen para rodar os 3 experimentos do Algoritmo Genético e visualizar a integração com a LLM.


---

## ✒️ Autor - Kevin Makoto Shiroma
Projeto desenvolvido como parte da avaliação do **Tech Challenge - Fase 2**.


