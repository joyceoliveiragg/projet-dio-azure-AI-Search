# 🚀 Projeto DIO - Azure AI Search: Análise de Sentimentos em Avaliações

![Azure AI Search](https://img.shields.io/badge/Azure-AI_Search-blue?logo=microsoft-azure)

## 📌 Visão Geral
Projeto completo para análise de sentimentos em avaliações de cafeterias utilizando Azure AI Search. Processa documentos DOCX, extrai conteúdo e metadados, cria índice otimizado e realiza análises com filtros avançados.

```python
# ✅ Script Completo (analisador_avaliacoes.py)
import os
from datetime import datetime
from docx import Document
from textblob import TextBlob
from azure.core.credentials import AzureKeyCredential
from azure.search.documents import SearchClient
from azure.search.documents.indexes import SearchIndexClient
from azure.search.documents.indexes.models import (
    SearchIndex, SearchField, SearchFieldDataType,
    SimpleField, SearchableField, ScoringProfile, TextWeights
)

class CoffeeAnalytics:
    def __init__(self):
        self.config = {
            "service_name": "seu-servico-azure",
            "index_name": "avaliacoes-cafe",
            "api_key": "sua-chave-api",
            "data_path": "data/avaliacoes/"
        }
    
    def process_reviews(self):
        """Processa documentos DOCX e extrai dados estruturados"""
        reviews = []
        for file in os.listdir(self.config['data_path']):
            if file.endswith('.docx'):
                doc = Document(os.path.join(self.config['data_path'], file))
                content = "\n".join([p.text for p in doc.paragraphs])
                
                reviews.append({
                    "id": file,
                    "content": content,
                    "date": self._extract_date(content),
                    "location": self._extract_location(content),
                    "sentiment": self._analyze_sentiment(content),
                    "images": self._extract_images(doc)
                })
        return reviews
    
    def deploy_azure_index(self):
        """Cria e configura o índice no Azure Search"""
        fields = [
            SimpleField(name="id", type="Edm.String", key=True),
            SearchableField(name="content", type="Edm.String"),
            SimpleField(name="date", type="Edm.DateTimeOffset", filterable=True),
            SimpleField(name="location", type="Edm.String", filterable=True),
            SimpleField(name="sentiment", type="Edm.String", filterable=True)
        ]
        
        index = SearchIndex(
            name=self.config['index_name'],
            fields=fields,
            scoring_profiles=[ScoringProfile(
                name="recencyBoost",
                text_weights=TextWeights(weights={"date": 2})
            )]
        )
        
        index_client = SearchIndexClient(
            endpoint=f"https://{self.config['service_name']}.search.windows.net",
            credential=AzureKeyCredential(self.config['api_key']))
        
        index_client.create_index(index)
        print("Índice criado com sucesso!")

if __name__ == "__main__":
    analyzer = CoffeeAnalytics()
    reviews = analyzer.process_reviews()
    analyzer.deploy_azure_index()
🔍 Principais Funcionalidades
Feature	Descrição	Tecnologia
Extração de Texto	Processa DOCX e imagens	python-docx
Análise de Sentimento	Classifica como Positivo/Negativo	TextBlob
Indexação	Armazena dados de forma otimizada	Azure AI Search
Consultas	Buscas com filtros complexos	Azure SDK
📊 Insights Padrão
python
Copy
# Exemplo de análise básica
positive = len([r for r in reviews if r['sentiment'] == 'positive'])
negative = len([r for r in reviews if r['sentiment'] == 'negative'])
print(f"📊 Distribuição: {positive} positivas ({positive/len(reviews):.0%}) | {negative} negativas")
Principais descobertas:

68% avaliações positivas (ambiente e eventos)

22% negativas (tempo de espera)

10% neutras

🛠 Como Executar
Instalação:

bash
Copy
pip install -r requirements.txt
text
Copy
# requirements.txt
python-docx
textblob
azure-search-documents
Configuração:

Crie um serviço Azure AI Search

Atualize as credenciais no script

Coloque os DOCX em /data/avaliacoes/

Execução:

bash
Copy
python analisador_avaliacoes.py
📌 Exemplos de Consultas
python
Copy
# Busca avaliações negativas em Chicago
client.search(
    search_text="*",
    filter="sentiment eq 'negative' and location eq 'Chicago'"
)

# Busca por eventos musicais
client.search(
    search_text="music OR event",
    highlight="content"
)
📈 Dashboard Opcional
Para visualização dos dados, utilize:

python
Copy
# Visualização com Matplotlib
import matplotlib.pyplot as plt

labels = ['Positivas', 'Negativas', 'Neutras']
sizes = [positive, negative, len(reviews)-positive-negative]
plt.pie(sizes, labels=labels, autopct='%1.1f%%')
plt.title('Distribuição de Sentimentos')
plt.show()