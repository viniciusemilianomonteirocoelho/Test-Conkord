# Testes Funcionais — Swag Labs

## Objetivo

Este documento apresenta cenários de testes funcionais, estratégia de automação, avaliação de riscos e reporte de bug da plataforma Swag Labs.

---

# Casos de Teste

## CT01 — Carregamento da Página de Produtos

### Funcionalidade
Carregamento da página de produtos

### Cenário: Carregamento da página com sucesso

```gherkin
Dado que o utilizador acede à página de inventário
Quando a página termina de carregar
Então a lista de produtos deve ser apresentada
```

---

## CT02 — Adicionar Produtos ao Carrinho

### Funcionalidade
Adicionar produtos ao carrinho

### Cenário: Adicionar um produto

```gherkin
Dado que o utilizador está na página de produtos
Quando clica em "Add to cart" de um produto
Então o produto deve ser adicionado ao carrinho
E o ícone do carrinho deve apresentar "1"
```

---

# Estratégia para Automação

## Automação de API — Postman

### Fluxos prioritários
- Listagem de produtos
- Ordenação por nome/preço
- Carrinho (adicionar/remover produtos)

---

## Automação de Integração Backend + Frontend

### Validações
- UI a consumir a API corretamente
- Dados apresentados corretamente na interface

---

## Automação de UI — Playwright

### Fluxos prioritários
- Login
- Adicionar/remover produto
- Checkout básico

---

# Avaliação de Risco

## Fluxo de Login

### Riscos
- Utilizador não autentica
- Sessão expira incorretamente

### Impacto
Bloqueia todo o funil de compra.

### Prioridade
🔴 ALTÍSSIMA — Automatizar

---

## Adicionar Produto ao Carrinho

### Riscos
- Produto não é adicionado
- Quantidade incorreta

### Impacto
O utilizador não consegue concluir a compra, causando perda direta de receita.

### Prioridade
🔴 ALTÍSSIMA — Automatizar

---

## Persistência do Carrinho

### Riscos
- Itens desaparecem ao atualizar a página
- Carrinho não mantém estado entre navegações

### Impacto
Abandono de compra.

### Prioridade
🔴 ALTÍSSIMA — Automatizar

---

## Acesso ao Carrinho

### Riscos
- Ícone não atualiza
- Redirecionamento falha

### Impacto
O utilizador não consegue finalizar a compra.

### Prioridade
🟠 ALTA — Automatizar

---

## Adicionar / Remover Produtos

### Riscos
- Duplicação de itens
- Remoção falha
- Estado inconsistente

### Impacto
Carrinho incorreto pode gerar cobrança errada e problemas críticos no fluxo de compra.

### Prioridade
🔴 ALTÍSSIMA — Automatizar

---

# Bug Report — BUG 02

## Título
Sessão expira com frequência na página de login impedindo autenticação consistente.

---

## Ambiente de Teste

| Item | Informação |
|---|---|
| Plataforma | Swag Labs |
| Navegador | Chrome |
| Dispositivo | Desktop |
| URL | https://saucedemo.com |

---

## Descrição

Após um curto período, a sessão do utilizador expira, porém o sistema continua a tentar aceder à rota protegida `cart.html`.

Em vez de redirecionar corretamente para a página de login ou renovar a sessão, a aplicação apresenta a seguinte mensagem:

```text
Epic sadface: You can only access '/cart.html' when you are logged in.
```

Isto indica uma falha no tratamento de sessão expirada e validação de autenticação na navegação entre rotas protegidas.

---

## Passos para Reproduzir

1. Aceder à página de login
2. Inserir username e password válidos
3. Entrar na homepage
4. Permanecer alguns minutos sem interação
5. Atualizar a página

---

## Resultado Atual

- A mensagem abaixo é apresentada:

```text
Epic sadface: You can only access 'inventory.html' when you are logged in.
```

- O login é realizado com sucesso
- Após poucos minutos o utilizador é automaticamente desconectado

---

## Resultado Esperado

- O utilizador deve permanecer autenticado por mais tempo
- A sessão não deve expirar tão rapidamente
- O sistema deve tratar corretamente a expiração da sessão

---

## Impacto

- Bloqueia a conclusão da compra
- Impede testes e utilização da plataforma
- Afeta diretamente o fluxo principal (login → compra)

---

## Severidade

🔴 Alta

---

## Possíveis Causas (Hipóteses)

- Token de sessão expira prematuramente
- Problemas no gerenciamento de cookies/localStorage
- Timeout de sessão demasiado curto

---

## Evidência

- Screenshot anexado demonstrando a mensagem de erro apresentada na página de login.

