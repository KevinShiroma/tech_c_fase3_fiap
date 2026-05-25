# Tech Challenge - Fase 3: Fine-Tuning de LLM Médico e Orquestração de Estados com LangGraph

Este repositório contém o projeto da Fase 3 do Tech Challenge (Pós-Tech IA para Devs). O objetivo desta etapa foi elevar o sistema hospitalar a um nível superior de especialização e segurança através do Fine-Tuning de um modelo de linguagem de grande escala (LLM) com protocolos internos e da criação de um assistente virtual médico estruturado com base em grafos de estado (LangGraph).

## 📺 Demonstração do Projeto
* **Link para o YouTube:** 
* **Apresentação:** Treinamento do modelo customizado, execução do grafo clínico com tomada de decisão automatizada e validação da trilha de auditoria.

## 🛠️ Arquitetura do projeto

<img width="2944" height="1248" alt="image" src="https://github.com/KevinShiroma/tech_c_fase3_fiap/blob/main/arquitetura/FLOWS.png" />

O ecossistema foi projetado para operar com total governança de dados, unindo técnicas avançadas de especialização de modelos e orquestração determinística.

* **Especialização de IA:** Framework Unsloth para o fine-tuning quantizado em 4-bits do Llama-3-8b, alimentado pelo dataset médico curado MedQuAD.

* **Orquestração por Estados:** Framework LangGraph para modelar o fluxo de atendimento da equipe médica através de um grafo direcionado com tomada de decisão condicional.

* **Camada de Dados:** Banco relacional SQLite local atuando como repositório de prontuários clínicos e exames controlados.

* * **Governança & Compliance:** Módulo de auditoria assíncrona responsável por registrar cada transação e inferência no arquivo físico audit_trail.log.

## 📋 Sobre a Evolução (Fase 3)

O foco desta fase foi mitigar alucinações e garantir a segurança biológica e regulatória em ambiente hospitalar, dividindo o projeto em duas frentes complementares:

### 1. Fine-Tuning de LLM com Dados Médicos
Aprimoramos as respostas clínicas especializando o modelo Llama-3-8b-bnb-4bit via Unsloth:
* **Curadoria e Limpeza::** Pipeline em Pandas e expressões regulares (Regex) para remover tags poluídas, textos repetitivos de interfaces e dados nulos do dataset MedQuAD.
* **Formatação de Prompt:** Mapeamento estruturado das perguntas e respostas no padrão Alpaca Prompt Template.
* **Métricas de Otimização** O treinamento reduziu o Loss inicial de 1.93 para uma convergência saudável de 0.73 no Step 60, mitigando riscos de overfitting.

### 2. Orquestração e Guardrails de Segurança com LangGraph
Substituímos o encadeamento linear tradicional por um sistema baseado em grafos de estados (StateGraph) para garantir o cumprimento de protocolos clínicos:
* **Roteamento Dinâmico:** Ao consultar o prontuário do paciente, a função condicional router_pending_exams verifica o status dos exames em tempo real. Se houver qualquer exame com a flag PENDING, o grafo desvia compulsoriamente para o nó de salvaguarda exames_pendentes.
* **Travas de Segurança (Guardrails):** O sistema injeta dinamicamente regras de governança severas no prompt: proibição estrita de prescrição de medicamentos, obrigatoriedade de escrita na terceira pessoa e exigência de explicabilidade (cross-reference com métricas clínicas).

---

## 📂 Estrutura do Projeto

```text
/
├── fine_tuning.ipynb                  # Notebook de download, preprocessing e fine-tuning com Unsloth
├── tech_challenge_fase_3_langchain.ipynb # Notebook principal de execução no Google Colab
└── hospital_project/                  # Diretório do projeto modularizado gerado em tempo de execução
    ├── database/
    │   └── connection.py              # Inicialização do SQLite e ferramenta de extração de prontuários
    ├── models/
    │   └── custom_llm.py              # Pipeline do HuggingFace encapsulando o modelo LoRA treinado
    └── utils/
        └── logger.py                  # Subsistema de logging clínico e geração do rastro de auditoria
```

## 🚀 Guia de Execução

Pré-requisitos
* Ambiente Google Colab com acelerador T4 GPU habilitado.
* Conta no Google Drive vinculada para armazenamento e leitura dos pesos do modelo treinado.

Passo 1: Execução do Fine-Tuning <br>
1) Abra o arquivo fine_tuning.ipynb no Google Colab. <br>
2) Execute todas as células. O script fará o download do dataset, executará a limpeza com Regex, treinará o adaptador LoRA e salvará os pesos gerados diretamente no seu Google Drive.


Passo 2: Execução do Assistente Hospitalar (LangGraph) <br>
1) Abra o arquivo tech_challenge_fase_3_langchain.ipynb no Google Colab. <br>
2) Ajuste a variável caminho_salvamento para apontar para a pasta do seu Google Drive onde os pesos foram salvos no Passo 1.
3) Execute as células. O script irá:
* Construir fisicamente a estrutura de arquivos modularizada.
* Inicializar o banco de dados SQLite com dados sintéticos controlados.
* Compilar o grafo e exibir o diagrama visual da tomada de decisão.
* Executar a inferência para o paciente selecionado, acionando as travas de segurança e persistindo os resultados em audit_trail.log.
---

## ✒️ Autor - Kevin Makoto Shiroma
Projeto desenvolvido como parte da avaliação do **Tech Challenge - Fase 3**.


