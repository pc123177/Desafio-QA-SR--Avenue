# Teste Para QA Senior Avenue

Este projeto foi feito para o desafio da vaga de QA SR na Avenue utilizando o framework Maestro. 

## 🛠️ Pré-requisitos

Para executar este projeto, você precisa ter instalado:

- [Maestro CLI](https://maestro.mobile.dev/)
- [Android Studio](https://developer.android.com/studio) 


## 📥 Instalação

1. Clone o repositório:
   ```bash
   git clone https://github.com/seu-usuario/Desafio-QA-SR--Avenue.git
   ```

2. Acesse o diretório do projeto:
   ```bash
   cd Desafio-QA-SR--Avenue
   ```

3. Instale o Maestro CLI:
   ```bash
   curl -Ls "https://get.maestro.mobile.dev" | bash
   ```

## 📱 Configuração do Ambiente

### Android
1. Configure as variáveis de ambiente do Android:
   ```bash
   export ANDROID_HOME=$HOME/Android/Sdk
   export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools
   ```

## ▶️ Executando os Testes

### Executar um teste específico:
```bash
maestro test ./tests/nome-do-teste.yaml
```

## 📁 Estrutura do Projeto

```
├── elements/              # Arquivos de PageObjects
├── tests/            # Arquivos de fluxo de teste
├── .gitignore/          # Arquivo de configuração para não subida de arquivos no git
└── README.md
```

## 📝 Criando Novos Testes

### Estrutura Page Object Model (POM)

Antes de criar um novo teste, siga estas etapas:

1. **Verificar Elementos Existentes**
   - Verifique na pasta `elements/` se os elementos da página que você vai testar já estão mapeados
   - Caso não estejam, crie um novo arquivo `.js` com o nome da página

2. **Mapeamento de Elementos**
   - Crie um arquivo `.js` na pasta `elements/` seguindo o padrão de nomenclatura da página
   - Exemplo de mapeamento (`elements/CompraDeAcoes.js`):

```javascript
output.CompraDeAcoes = {
    SelectStockList: "Select Stock",
    AlphabetIncList: "Alphabet Inc. (GOOGL)",
    QuantityButton: "Quantity",
    BuyStockButton: "Buy Stock",
    PurchaseSuccessfulMessage: "Purchase Successful"
}
```

3. **Atualizar LoadElements**
   - Após criar o arquivo de elementos, adicione-o ao arquivo `loadElements.yaml`:

```yaml
appId: com.example.stock_app
---
- runScript: Cadastro.js
- runScript: Login.js
- runScript: Home.js
- runScript: CompraDeAcoes.js
```

### Criando o Teste

Após o mapeamento dos elementos, crie seu teste em formato YAML. Exemplo básico:

```yaml
appId: com.example.stock_app
---
- runFlow: ..\elements\LoadElements.yaml
- launchApp:
        appId: "com.example.stock_app"
        stopApp: true
        clearState: true
- tapOn: ${output.login.UsuarioInput}
- inputText: "Teste"
- tapOn: ${output.login.SenhaInput}
- inputText: "Teste"
- tapOn: ${output.login.EntrarButton}
- assertVisible: ${output.home.BemVindoMensagem}

```

### Boas Práticas

1. Mantenha os elementos organizados por página
2. Use nomes descritivos para os elementos
3. Mantenha o arquivo `loadElements.yaml` atualizado
4. Reutilize elementos já mapeados quando possível
5. Siga o padrão de nomenclatura estabelecido no projeto