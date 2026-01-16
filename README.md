# Sistemas Monolito — Guia de Execução e Testes

Este projeto implementa um monólito didático com módulos (Client Adm, Product Adm, Store Catalog, Invoice e Payment) seguindo conceitos de DDD, facades e use cases. Não há um servidor HTTP dedicado; a validação do comportamento é feita via suíte de testes automatizados.

## Pré-requisitos
- Node.js 16+ (recomendado 18 ou superior)
- npm 8+
- Sistema operacional: Windows, macOS ou Linux (testado no Windows)

## Instalação
1. Instale as dependências:

```bash
npm install
```

## Como executar (build) 
- Transpilar TypeScript para `dist/`:

```bash
npm run tsc
```

> Observação: o build não inicia um servidor; ele apenas gera artefatos JavaScript em `dist/`.

## Como testar (todos os módulos)
- Rodar toda a suíte de testes e checagem de tipos:

```bash
npm test
```

O comando acima primeiro roda o TypeScript (`tsc --noEmit`) para garantir tipos corretos, e depois executa o Jest. Os testes usam SQLite em memória, portanto não há necessidade de configurar banco de dados externo.

### Rodar testes em modo observação (opcional)
```bash
npx jest --watchAll
```

### Rodar testes de um módulo específico (opcional)
Exemplos:
- Client Adm (repositório):
```bash
npx jest src/modules/client-adm/repository/client.repository.spec.ts
```
- Product Adm (use cases):
```bash
npx jest src/modules/product-adm/usecase/add-product/add-product.usecase.spec.ts
```
- Store Catalog (facade):
```bash
npx jest src/modules/store-catalog/facade/store-catalog.facade.spec.ts
```
- Invoice (use cases):
```bash
npx jest src/modules/invoice/usecase/find-invoice/find-invoice.usecase.spec.ts
```
- Payment (facade):
```bash
npx jest src/modules/payment/facade/payment.facade.spec.ts
```

## Estrutura principal
- `src/modules/client-adm`: cadastro e consulta de clientes
- `src/modules/product-adm`: cadastro e checagem de estoque
- `src/modules/store-catalog`: catálogo para consulta
- `src/modules/invoice`: geração e consulta de faturas
- `src/modules/payment`: processamento de pagamentos

## Dicas e solução de problemas
- Caso haja erros de tipagem, verifique a versão do Node.js e reinstale dependências:
```bash
npm ci
```
- Se o Jest não encontrar testes, assegure-se de estar na raiz do projeto.
- Em ambientes corporativos com proxy, configure variáveis de ambiente do npm conforme necessário.

## Observação
Este repositório foca na lógica de domínio e integrações via facades e repositórios. A execução "da aplicação" é representada pelos testes automatizados cobrindo os fluxos principais de cada módulo.
