# **Synapse: Intelligence-Driven Knowledge Distillation**

## **1\. Visão Geral e Objetivos (O Pitch)**

**Synapse** é uma ferramenta CLI open-source projetada para atuar como a ponte entre fluxos de conversas efêmeras (Google Takeout/Gemini) e um sistema de conhecimento persistente (**Obsidian**).

Diferente de simples conversores, o Synapse utiliza agentes inteligentes para:

* **Destilar** conversas brutas em notas atômicas.  
* **Mapear** o conhecimento através de índices em cascata.  
* **Evoluir** um perfil de identidade do usuário (preferências, stack técnica e interesses) de forma iterativa.

## **2\. Requisitos e Casos de Uso**

* **Input:** Arquivos JSON (padrão Google Takeout).  
* **Output:** Um Vault Obsidian estruturado e autossuficiente.  
* **Idempotência:** Não processar a mesma conversa duas vezes (verificação via hash/ID no manifesto).  
* **Preservação de Tom:** Manter a personalidade e o estilo de escrita do usuário nas notas geradas.  
* **Navegação Inteligente:** Criação automática de links bidirecionais \[\[ \]\].

## **3\. Especificação Técnica e Arquitetura**

### **3.1 Padrões de Projeto (Design Patterns)**

* **Adapter Pattern:** Para a camada de entrada de dados (Input Drivers).  
* **Bridge Pattern:** Para a integração com LLMs, permitindo troca de provedores.  
* **Strategy Pattern:** Para diferentes métodos de organização.

### **3.2 Stack Tecnológica**

* **Linguagem:** Python 3.10+ (Ambiente Linux).  
* **Orquestração de Agentes:** **CrewAI**.  
* **Persistência de Estado:** synapse-manifest.json (Localizado na raiz do Vault).  
* **Interface:** CLI (via click ou argparse).

### **3.3 Estrutura de Pastas do Vault (Output)**

```
/SecondBrain (Raiz)  
├── synapse-manifest.json    \# Cache de processamento e metadados  
├── Index.md                 \# Índice Geral (Grand Central)  
├── /Journal/                \# Conversas datadas e logs  
│   └── Index.md             \# Índice cronológico  
├── /Atlas/                  \# Notas atômicas de conhecimento  
│   └── Index.md             \# Índice temático/MOC  
├── /Identity/               \# Perfil do usuário e preferências  
│   ├── User\_Profile.md      \# Nota central de identidade  
│   └── Index.md             \# Índice de evolução de interesses  
└── /Meta/                   \# Configurações do Synapse e templates
```

## **4\. Lógica de Processamento e Comportamento**

### **4.1 Divisão de Notas (Atomicidade)**

O agente **Distiller** deve identificar mudanças semânticas de assunto dentro de uma mesma conversa.

* **Critério:** Se o tópico mudar drasticamente, o software gera arquivos .md distintos na pasta /Atlas.

### **4.2 Gestão de Identidade e Conflitos**

O agente **Librarian** deve atualizar o User\_Profile.md:

* **Novas Informações:** Adicionadas às seções respectivas.  
* **Contradições:** Informação antiga movida para \#\# History/Archive, nova assume o topo.

### **4.3 Preservação de Tom de Voz**

* Uso de *Few-Shot Prompting* para replicar o estilo original (casual, técnico, etc).

## **5\. Agentes e Tarefas (CrewAI)**

1. **The Distiller:** Extrai conhecimento e formata em Markdown.  
2. **The Librarian:** Gerencia índices, links e perfil de identidade.

## **6\. Plano de Execução Detalhado (Milestones)**

### **Milestone 1: Foundation & Bootstrapping (A Base)**

* \[ \] Setup do ambiente (venv, requirements.txt, estrutura de pastas do projeto).  
* \[ \] Implementar CLI básica para capturar caminhos de \--input e \--output.  
* \[ \] Criar motor de Bootstrap: função que detecta se o Vault existe ou cria a árvore /Journal, /Atlas, /Identity, /Meta.  
* \[ \] Inicializar synapse-manifest.json com schema padrão e controle de versão.  
* \[ \] Gerar os arquivos Index.md iniciais com frontmatter YAML básico.  
* \[ \] Implementar o Loader de JSON para o formato específico do Google Takeout.  
* \[ \] Lógica de filtragem: comparar IDs do JSON com o manifesto para ignorar conversas já processadas.

### **Milestone 2: Intelligence & Formatting (O Cérebro)**

* \[ \] Configurar variáveis de ambiente e autenticação com a API do Gemini.  
* \[ \] Definir a classe de Agente Distiller com seu papel e ferramentas.  
* \[ \] Desenvolver o prompt de sistema do Distiller com foco em extração atômica e tom de voz.  
* \[ \] Implementar utilitário de escrita de Markdown (Markdown Writer) que garanta propriedades YAML compatíveis com Obsidian.  
* \[ \] Criar fluxo de teste: converter uma conversa única do JSON em um arquivo .md estruturado.

### **Milestone 3: Connectivity & Identity (A Memória)**

* \[ \] Definir a classe de Agente Librarian e suas responsabilidades de curadoria.  
* \[ \] Implementar leitor de User\_Profile.md para carregar contexto atual do usuário.  
* \[ \] Desenvolver tarefa do Librarian para comparar novas notas com o perfil e identificar atualizações.  
* \[ \] Lógica de Gestão de Conflitos: mover informações obsoletas para o arquivo de Archive/History.  
* \[ \] Sistema de Auto-Link: escanear títulos existentes no /Atlas e sugerir links \[\[ \]\] nas novas notas.  
* \[ \] Atualização automática de índices em cascata (adicionar novas entradas nos Index.md).

### **Milestone 4: Refinement & Open Source (A Entrega)**

* \[ \] Abstrair chamadas de LLM (Adapter Pattern) para permitir troca de modelos.  
* \[ \] Implementar sistema de Logs para acompanhar o progresso do processamento no terminal.  
* \[ \] Adicionar tratamento de erros (timeouts de API, JSON corrompido).  
* \[ \] Escrever README.md com instruções de instalação, configuração e guia de contribuição.  
* \[ \] Criar suite de testes unitários para o parser de JSON e lógica de idempotência.
