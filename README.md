# projet-dio-azure-AI-Search

## Análise de Sentimentos em Avaliações de Cafeteria com Azure AI Search

### 📌 Visão Geral do Projeto

Este projeto demonstra como utilizar o **Azure AI Search** para analisar avaliações de clientes de uma cafeteria fictícia chamada **"Fourth Coffee"**. O objetivo é:

- Organizar os documentos em um repositório pesquisável
- Criar um índice eficiente para consultas
- Realizar pesquisas com **filtros por sentimentos** (positivo/negativo/neutro) e **localização**

---

### ⚙️ Passo a Passo para Configuração

#### 1. Ingestão de Dados

##### 🔄 Processo:

- Coletar avaliações em formato **DOCX**
- Extrair o **conteúdo textual**
- Processar **imagens associadas** (quando aplicável), extraindo **metadados**
- Estruturar os dados em um formato padronizado contendo:

  - 📄 Conteúdo da avaliação  
  - 📅 Data  
  - 📍 Localização (cidade, estado)  
  - 😀 Sentimento (positivo/negativo/neutro)  

---

### 💡 Insights Obtidos

#### 📊 Distribuição de Sentimentos:

- A maioria das avaliações é **positiva**, destacando:
  - Eventos culturais
  - Ambiente acolhedor
  - Qualidade do café
- As críticas negativas concentram-se em:
  - Tempos de espera
  - Lotação nos fins de semana

#### 🔁 Tópicos Frequentes:

- 🎶 Eventos culturais (música, arte)  
- 🧑‍💻 Espaço para trabalho/reuniões  
- 🍽️ Opções de comida rápida  
- ☕ Ambiente acolhedor  

#### 🌎 Diferenças Regionais:

- **Seattle**: ênfase em **arte local** e **eventos familiares**  
- **Chicago**: foco em **reuniões de negócios**  
- **Los Angeles**: popular entre **estudantes universitários**  

---

### 🚀 Possíveis Melhorias

#### 🧠 Enriquecimento de IA:

- Extração automática de **palavras-chave**
- Identificação de **tópicos principais**
- Classificação das avaliações por categorias:
  - Comida
  - Serviço
  - Ambiente

#### 📈 Visualização de Dados:

- 🗺️ Mapa de calor por **localização/sentimento**
- 🕒 Linha do tempo com volume e polaridade de avaliações
- ☁️ Nuvem de palavras com os tópicos mais citados

#### 🔗 Integrações:

- Integração com **CRM** para acompanhamento de avaliações negativas
- **Alertas automáticos** para tendências negativas emergentes

---

### 📚 Aprendizados

- **Pré-processamento é essencial**: padronizar formatos de data e localização foi fundamental para a eficácia dos filtros.
- **Análise de sentimentos agrega valor**: permite identificar rapidamente problemas e pontos fortes sem leitura manual.
- **Azure AI Search é altamente flexível**: combinação de **full-text search** com filtros estruturados é poderosa para análise.
- **Contexto importa**: avaliações com palavras similares podem ter polaridades diferentes — análises mais sofisticadas são necessárias para capturar nuances (ex.: “lotação” pode ser positiva ou negativa, dependendo do contexto).

---

### ✅ Conclusão

Este projeto mostra como o uso de ferramentas de IA e serviços cognitivos da Azure pode transformar grandes volumes de dados textuais em **insights acionáveis**, fornecendo suporte para **melhoria de serviços, marketing direcionado e decisões estratégicas**.

---

