Markdown# EcoBite 🌿🍎

> Aplicação em Flutter desenvolvida para o combate ao desperdício alimentar, permitindo a gestão inteligente da despensa, alertas de validade, registo de consumos/descartes e sugestão de receitas baseadas nos ingredientes disponíveis.
🎯 Sobre o ProjetoO EcoBite é uma solução completa para organizar alimentos em casa, priorizar o consumo de itens próximos do vencimento e gerar métricas sobre hábitos de consumo contra desperdício de comida.🚀 Como Executar o ProjetoClonar o repositório:Bashgit clone [https://github.com/seu-usuario/ecobite.git](https://github.com/seu-usuario/ecobite.git)
cd ecobite
Instalar as dependências:Bashflutter pub get
Executar no Navegador (Web / Localhost):Bashflutter run -d edge
# ou
flutter run -d chrome
Executar num Dispositivo Móvel:Bashflutter run
💡 Nota sobre cache na Web: O Flutter Web pode guardar cache agressivo de build no navegador. Se uma alteração não surgir após o reinício, execute flutter clean e depois flutter pub get antes de executar novamente.🧱 Estrutura do projetoPlaintextlib/
├── main.dart                          # MaterialApp, rotas nomeadas, MultiProvider
├── models/
│   ├── alimento_model.dart            # Modelo Alimento (parse JSON / Map SQLite)
│   ├── historico_baixa_model.dart     # Modelo de registo de baixa (Consumido/Descartado)
│   └── receita_model.dart             # Modelo de receita da Spoonacular
├── services/
│   ├── database_service.dart          # Singleton + SQL puro (SQLite mobile / memória Web)
│   ├── open_food_facts_service.dart   # Integração com API Open Food Facts (código de barras)
│   └── spoonacular_service.dart       # "SpoonacularService" — chamadas HTTP + fallback local
├── providers/
│   └── despensa_provider.dart         # Estado da Despensa (CRUD, baixas e histórico)
├── routes/
│   └── app_routes.dart                # Centralização das rotas nomeadas da aplicação
└── views/
    ├── despensa_screen.dart           # RF03, RF04, RF07 — lista da despensa, alertas e baixa
    ├── cadastro_alimento_screen.dart  # RF01, RF02 — formulário e scanner de código de barras
    ├── estatisticas_screen.dart       # RF08 — métricas de consumo vs descarte
    └── receitas_screen.dart           # RF05, RF06 — recomendações e detalhes de receitas
🗺️ Rotas nomeadasRotaTela/Home (DespensaScreen) — lista de alimentos ordenados por validade/cadastroCadastro (CadastroAlimentoScreen) — formulário manual e código de barras/estatisticasEstatísticas (EstatisticasScreen) — gráficos de consumo vs. descarte/receitasReceitas (ReceitasScreen) — sugestões com base na despensa📱 💻 Responsividade< 700px (celular): AppBar com ações de navegação + lista de cards com indicador semafórico de validade + FloatingActionButton para acesso rápido ao cadastro.700–1099px (tablet): Diálogos modais centralizados e adaptativos para ajuste de quantidade e seleção do motivo da baixa.≥ 1100px (desktop / janela larga no navegador): Layout estendido em localhost com visualização panorâmica da despensa e navegação rápida entre relatórios estatísticos e receitas.💾 Banco de dados (SQLite)Duas tabelas, mesmo padrão (DatabaseService singleton + SQL puro no Mobile / armazenamento em memória com kIsWeb na Web):SQLCREATE TABLE alimentos (
  id TEXT PRIMARY KEY,
  nome TEXT NOT NULL,
  categoria TEXT NOT NULL,
  dataValidade TEXT NOT NULL,
  quantidade REAL NOT NULL,
  unidadeMedida TEXT NOT NULL,
  fotoUrl TEXT
);

CREATE TABLE historico_baixas (
  id TEXT PRIMARY KEY,
  alimentoId TEXT NOT NULL,
  nomeAlimento TEXT NOT NULL,
  quantidade REAL NOT NULL,
  motivo TEXT NOT NULL,
  dataBaixa TEXT NOT NULL
);
id PRIMARY KEY garante que cada item e registo de histórico tenham identificadores únicos sem duplicidade (ConflictAlgorithm.replace).A tabela historico_baixas guarda a quantidade e o motivo obrigatório (Consumido ou Descartado) em cada remoção de estoque para alimentar a tela de estatísticas (RN05).Suporte Dual (Web/Mobile): Ao executar no navegador, a aplicação alterna automaticamente para persistência em memória volátil, evitando erros de suporte do driver SQLite nativo.🌐 Sobre a busca de receitas no SpoonacularSpoonacularService.buscarReceitasPorIngredientes cruza os alimentos presentes na despensa para sugerir receitas personalizadas, priorizando os produtos prestes a vencer (RN02). Se a API externa estiver sem chave, indisponível ou com limite de requisições excedido, o serviço aciona um fallback com catálogo local de receitas para garantir que a interface continue funcional sem exibir erros ao utilizador.✅ Requisitos atendidosRF01 Cadastrar Alimento — formulário manual com validação de campos na rota /cadastroRF02 Leitura de Código de Barras — consulta via API Open Food Facts para preenchimento automáticoRF03 Listar Despensa — ordenação automática dos alimentos por data de vencimento na rota /RF04 Dar Baixa no Estoque — diálogo com quantidade customizada e seleção do motivo (RN05)RF05 Recomendar Receitas — consulta por ingredientes via Spoonacular ou catálogo local na rota /receitasRF06 Detalhar Receita — exibição expandida com ingredientes necessários e modo de preparoRF07 Alertas Visuais de Validade — indicador por cores (Verde: Normal | Laranja: ≤ 3 dias | Vermelho: Vencido/Hoje)RF08 Estatísticas e Métricas — painel visual com taxa de consumo vs. descarte na rota /estatisticas
