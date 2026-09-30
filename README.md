# EcoBite 🌿🍎
EcoBite é uma aplicação desenvolvida em Flutter focada no combate ao desperdício de alimentos. A plataforma permite gerir os itens da despensa, acompanhar datas de validade através de alertas visuais, registar o destino dos alimentos (consumo vs. descarte) e obter recomendações de receitas personalizadas com base nos ingredientes disponíveis.

🚀 Funcionalidades Principais
📦 Gestão de Despensa: Registo manual de alimentos e suporte para leitura de código de barras (via Open Food Facts).

⏳ Acompanhamento de Validades: Notificação visual semafórica baseada no tempo restante para o vencimento:

🔴 Crítico: Vencido ou vence hoje.

🟠 Atenção: Vence em até 3 dias.

🟢 Normal: Dentro do prazo de validade.

📉 Registo de Baixa Obrigatório: Registo de saídas de stock especificando a quantidade e o motivo (Consumido ou Descartado).

📊 Estatísticas e Métricas: Painel visual para acompanhamento da taxa de consumo contra a taxa de desperdício.

🍳 Sugestão de Receitas: Integração com a API da Spoonacular para recomendar receitas utilizando prioritarimente os alimentos que estão prestes a vencer, contando com suporte a fallback local para funcionamento offline.

🌐 Suporte Multiplataforma (Dual-Database): Persistência de dados nativa em SQLite para dispositivos móveis (Android/iOS) e suporte a armazenamento em memória para execução na Web (localhost).

🛠️ Tecnologias Utilizadas
Framework: Flutter (Dart)

Gestão de Estado: Provider

Navegação & Rotas: Rotas nomeadas centralizadas (AppRoutes)

Base de Dados:

sqflite (Ambiente Mobile)

Memória Volátil / kIsWeb (Ambiente Web)

Consumo de APIs:

http

Spoonacular API

Open Food Facts API

📁 Estrutura do Projeto
Plaintext
lib/
├── models/             
├── providers/            
├── routes/               
├── services/             
└── views/                

models: Modelos de dados (Alimento, HistoricoBaixa, Receita) /n
providers: Estado global e regras de negócio (DespensaProvider)
routes: Configuração centralizada de rotas (AppRoutes)
services: Comunicação com APIs e Base de Dados (DatabaseService, SpoonacularService, etc.)
views: Ecrãs da aplicação (Despensa, Cadastro, Estatísticas, Receitas)


🔧 Como Executar o Projeto
Pré-requisitos
Flutter SDK instalado.

Navegador (Google Chrome ou Microsoft Edge) ou emulador Android/iOS configurado.

Passos
Clonar o repositório:

Bash
git clone https://github.com/seu-usuario/ecobite.git
cd ecobite
Instalar as dependências:

Bash
flutter pub get
Executar na Web (Navegador):

Bash
flutter run -d edge
# ou
flutter run -d chrome
Executar no Dispositivo Móvel:

Bash
flutter run
🔑 Configuração de API (Opcional)
Para habilitar a busca completa de receitas em tempo real via API externa:

Registe-se em Spoonacular API Console para obter uma chave gratuita.

Adicione a sua chave no ficheiro lib/services/spoonacular_service.dart:

Dart
static const String _apiKey = 'SUA_CHAVE_AQUI';
(Nota: Se a chave não for informada ou houver falha de conexão, a aplicação utilizará automaticamente o catálogo interno de receitas de contingência).
