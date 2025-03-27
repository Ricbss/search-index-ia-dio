Configuração e Utilização do Azure AI Search
Este repositório contém um guia detalhado para configurar e utilizar o Azure AI Search, explorando um índice de pesquisa baseado em dados extraídos de avaliações de clientes. Este documento abrange o processo de criação de recursos, enriquecimento de dados com inteligência artificial e consulta a um índice de pesquisa.

1. Recursos Necessários
Para implementar essa solução, você precisará dos seguintes recursos no Azure:

Azure AI Search: Para gerenciar indexação e consultas.
Azure AI Services: Para aplicar habilidades de IA ao enriquecimento dos dados.
Azure Storage Account: Para armazenar documentos brutos e dados indexados.
Importante: Certifique-se de que os recursos do Azure AI Search e Azure AI Services estão na mesma região!

2. Criando os Recursos no Azure
2.1 Criar um Recurso Azure AI Search
Acesse o Portal Azure.
Clique em + Criar um recurso e pesquise por Azure AI Search.
Configure com as seguintes definições:
Subscription: Sua assinatura do Azure.
Resource Group: Crie ou selecione um grupo de recursos.
Service Name: Um nome único.
Location: Escolha uma região disponível.
Pricing Tier: Basic.
Clique em Review + Create e depois em Create.
Após a implantação, vá para o recurso criado.
2.2 Criar um Recurso Azure AI Services
Retorne à home do portal Azure.
Clique em + Criar um recurso e pesquise por Azure AI Services.
Configure com:
Resource Group: O mesmo do Azure AI Search.
Location: A mesma região do Azure AI Search.
Pricing Tier: Standard S0.
Clique em Review + Create e depois em Create.
2.3 Criar uma Storage Account
No portal Azure, clique em + Criar um recurso e pesquise por Storage Account.

Configure com:

Resource Group: O mesmo dos recursos anteriores.
Storage Account Name: Um nome único.
Performance: Standard.
Redundancy: Locally Redundant Storage (LRS).
Clique em Review + Create e depois em Create.

No recurso criado, vá até Configurações > Configuração e ative Allow Blob Anonymous Access.

3. Carregando Dados no Azure Storage
No Storage Account, vá para Containers.
Clique em + Container e crie:
Name: coffee-reviews.
Public access level: Container.
Faça o download dos arquivos de exemplo aqui e extraia.
No container coffee-reviews, clique em Upload e carregue os arquivos.
4. Indexação dos Documentos
No Azure AI Search, clique em Import Data.

Escolha Azure Blob Storage como fonte de dados e configure:

Data Source Name: coffee-customer-data.
Data to Extract: Content and Metadata.
Parsing Mode: Default.
Connection String: Escolha sua conta de armazenamento e container coffee-reviews.
Clique em Next: Add Cognitive Skills e selecione:

Skillset Name: coffee-skillset.
Habilidades de IA:
OCR e Merged Content.
Extract Location Names.
Extract Key Phrases.
Detect Sentiment.
Generate Tags from Images.
Generate Captions from Images.
Em Save Enrichments to a Knowledge Store, selecione:

Image Projections.
Documents.
Pages.
Key Phrases.
Entities.
Crie um container knowledge-store para armazenar os dados processados.

Clique em Next: Customize Target Index, defina:

Index Name: coffee-index.
Key: metadata_storage_path.
Marque campos como Filterable para content, locations, keyphrases, sentiment, merged_content.
Clique em Next: Create an Indexer e defina:

Indexer Name: coffee-indexer.
Schedule: Once.
Base-64 Encode Keys: Yes.
Clique em Submit e aguarde a conclusão.

5. Consultando o Índice de Pesquisa
5.1 Usando o Search Explorer
No Azure AI Search, clique em Search Explorer.
No editor JSON, cole:
{
    "search": "*",
    "count": true
}
Clique em Search para visualizar os documentos indexados.

Para filtrar por localização:

{
    "search": "locations:'Chicago'",
    "count": true
}
Para filtrar por sentimento negativo:
{
    "search": "sentiment:'negative'",
    "count": true
}
6. Revisão do Knowledge Store
No Storage Account, acesse o container knowledge-store.
Veja os arquivos JSON armazenados, incluindo metadados e projeções de imagem.
📌 Insights e Aplicações
🔍 Benefícios do Azure AI Search
Automação da análise de dados: Insights extraídos automaticamente.
Pesquisa poderosa: Busca eficiente mesmo em grandes volumes de dados.
IA integrada: Sentimento, palavras-chave e reconhecimento de imagem.
Escalabilidade: Pode ser expandido para mais fontes e aplicações.
🚀 Possibilidades de Aplicação
Chatbots: Respostas mais inteligentes baseadas em feedbacks.
E-commerce: Busca avançada em catálogos.
Monitoramento de Redes Sociais: Análise de sentimentos e tendências.
Pesquisas Acadêmicas: Indexação de artigos e documentos.
📚 Aprendizados
Durante essa configuração, aprendemos:

Como configurar uma pesquisa inteligente no Azure AI Search.
Como enriquecer documentos com Azure AI Services.
Como armazenar e gerenciar dados estruturados em Azure Storage.
Como utilizar a busca avançada para extrair insights valiosos.
Esse processo pode ser aplicado em diversos contextos, trazendo poder analítico para empresas que lidam com grandes volumes de informação.

🔗 Dúvidas ou sugestões? Contribua no repositório! 🚀
