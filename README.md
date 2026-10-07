<div align="center">

# 🌿 EcoBite 🍎

**Menos desperdício, mais aproveitamento.**

![Flutter](https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white)
![Dart](https://img.shields.io/badge/Dart-0175C2?style=for-the-badge&logo=dart&logoColor=white)
![SQLite](https://img.shields.io/badge/SQLite-003B57?style=for-the-badge&logo=sqlite&logoColor=white)

![Stars](https://img.shields.io/github/stars/SeuUser/ecobite?style=social)
![License](https://img.shields.io/github/license/SeuUser/ecobite)
![Top Language](https://img.shields.io/github/languages/top/SeuUser/ecobite)

</div>

---

## 📖 Sobre o projeto

O **EcoBite** é uma aplicação desenvolvida em **Flutter** focada no combate ao desperdício de alimentos. A plataforma permite gerenciar os itens da despensa, acompanhar datas de validade por meio de alertas visuais, registrar o destino dos alimentos (**consumo vs. descarte**) e obter recomendações de receitas personalizadas com base nos ingredientes disponíveis.

![Preview](https://link-da-imagem.com/preview.png)

---

## 🚀 Funcionalidades principais

- 📦 **Gestão de despensa:** cadastro manual de alimentos e leitura de código de barras (via Open Food Facts).
- ⏳ **Acompanhamento de validades:** alerta visual semafórico conforme o tempo restante até o vencimento.
- 📉 **Registro de baixa obrigatório:** toda saída de estoque informa a quantidade e o motivo (*Consumido* ou *Descartado*).
- 📊 **Estatísticas e métricas:** painel visual com a taxa de consumo contra a taxa de desperdício, incluindo um gráfico por alimento.
- 🍳 **Sugestão de receitas:** integração com a API da Spoonacular, priorizando os alimentos que estão prestes a vencer. Títulos, ingredientes e modo de preparo são traduzidos para português, e há um catálogo local de contingência para quando a API estiver indisponível.
- 🌐 **Suporte multiplataforma (dual-database):** persistência nativa em SQLite no mobile (Android/iOS) e armazenamento em memória na Web (localhost).

### 🚦 Semáforo de validade

| Status | Cor | Regra |
|--------|-----|-------|
| **Crítico** | 🔴 | Vencido ou vence hoje |
| **Atenção** | 🟠 | Vence em até 3 dias |
| **Normal** | 🟢 | Dentro do prazo de validade |

---

## 🛠️ Tecnologias utilizadas

| Categoria | Tecnologia |
|-----------|------------|
| Framework | Flutter (Dart) |
| Gerenciamento de estado | Provider |
| Navegação | Rotas nomeadas centralizadas (`AppRoutes`) |
| Banco de dados | `sqflite` (mobile) e memória volátil via `kIsWeb` (web) |
| Consumo de APIs | `http` |
| Gráficos | `fl_chart` |
| Leitura de código de barras | `mobile_scanner` |

### 🔌 APIs externas

- 🍳 [Spoonacular API](https://spoonacular.com/food-api): busca de receitas por ingredientes.
- 🥫 [Open Food Facts](https://world.openfoodfacts.org/): dados de produtos por código de barras.
- 🌐 [MyMemory](https://mymemory.translated.net/): tradução das receitas para português.

---

## 📁 Estrutura do projeto

```text
lib/
├── models/
  ├── alimento_model.dart
  ├── historico_baixa.dart
  ├── receita_model.dart
├── providers/
  ├── despensa_provider.dart
├── routes/
  ├── app_routes.dart
├── services/
  ├── database_serivce.dart
  ├── open_food_facts_service.dart
  ├── spoonacular_service.dart
  ├── translation_service.dart
├── theme/
  ├── app_theme.dart
├── views/
  ├── cadastro_alimento_screnn.dart
  ├── despensa_screen.dart
  ├── estatisticas_screen.dart
  ├──receitas_screen.dart
├── widgets/
  ├── app_bottom.dart
  ├── receita_card.dart
└── main.dart
```

- **`models`**: modelos de dados (`Alimento`, `HistoricoBaixa`, `Receita`).
- **`providers`**: estado global e regras de negócio (`DespensaProvider`).
- **`routes`**: configuração centralizada de rotas (`AppRoutes`).
- **`services`**: comunicação com APIs e banco de dados (`DatabaseService`, `SpoonacularService`, `OpenFoodFactsService`, `TranslationService`).
- **`theme`**: identidade visual do app (`AppTheme`).
- **`views`**: telas da aplicação (Despensa, Cadastro, Estatísticas, Receitas).
- **`widgets`**: componentes reutilizáveis (barra de navegação inferior).

---

## 🔧 Como executar o projeto

### Pré-requisitos

- [Flutter SDK](https://docs.flutter.dev/get-started/install) instalado.
- Navegador (Google Chrome ou Microsoft Edge) **ou** emulador Android/iOS configurado.

### Passo a passo

1. Clone o repositório:

```bash
git clone https://github.com/seu-usuario/ecobite.git
cd ecobite
```

2. Instale as dependências:

```bash
flutter pub get
```

3. Execute na Web (navegador):

```bash
flutter run -d edge
# ou
flutter run -d chrome
```

4. Execute em um dispositivo móvel:

```bash
flutter run
```

---

## 🔑 Configuração de API (opcional)

Para habilitar a busca completa de receitas em tempo real:

1. Cadastre-se no [Spoonacular API Console](https://spoonacular.com/food-api/console) e obtenha uma chave gratuita.
2. Adicione a sua chave no arquivo `lib/services/spoonacular_service.dart`:

```dart
static const String _apiKey = 'SUA_CHAVE_AQUI';
```

> ⚠️ **Atenção:** nunca publique a sua chave real no GitHub. Use uma chave de teste ou mantenha-a fora do repositório.

> 📝 **Nota:** se a chave não for informada ou houver falha de conexão, a aplicação usa automaticamente o catálogo interno de receitas de contingência.

---

## 🌟 Dica final

Cada alimento aproveitado é menos lixo no planeta. 🌍 Use o **EcoBite** para comprar melhor, cozinhar mais e desperdiçar menos!

---

<div align="center">

Feito com 💚 e Flutter

</div>
