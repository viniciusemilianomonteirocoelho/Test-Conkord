# Test Conkord Swag Labs

Portal de e-commerce de itens de moda

## Funcionalidades
- Login
- Adicionar itens ao carrinho
- Remover itens do carrinho
- Menu com abas laterais
- Validação de compra

## Instalação

### Pré-requisitos
- Google Chrome instalado
#  Casos de Teste – E-commerce

Este documento descreve os principais casos de teste funcionais realizados na aplicação de e-commerce, incluindo cenários positivos e validações de interface.

---

## 1.  Carregamento da Página de Produtos

### Cenário: Página carrega com sucesso
**Dado** que o usuário acessa a página de inventário  
**Quando** a página termina de carregar  
**Então** a lista de produtos deve ser exibida  


### Cenário: Elementos principais visíveis
**Dado** que o usuário está na página  
**Quando** a página é exibida  
**Então** deve conter:
- Título "Products"
- Menu lateral disponível
- Ícone do carrinho visível

---

## 2.  Exibição dos Produtos

### Cenário: Produtos possuem informações completas
**Dado** que o usuário está na página de produtos  
**Quando** os produtos são carregados  
**Então** cada produto deve conter:
- Nome
- Preço
- Imagem
- Botão "Add to cart"

---

### Cenário: Imagem do produto carregada corretamente
**Dado** que o usuário visualiza um produto  
**Quando** a imagem é exibida  
**Então** ela não deve estar quebrada

---

## 3.  Adicionar Produtos ao Carrinho

### Cenário: Adicionar um produto
**Dado** que o usuário está na página de produtos  
**Quando** clica em "Add to cart"  
**Então** o produto é adicionado ao carrinho  
E o ícone do carrinho exibe "1"

---

### Cenário: Adicionar múltiplos produtos
**Quando** o usuário adiciona 6 produtos  
**Então** o carrinho deve exibir "6"

---

### Cenário: Evitar duplicação
**Dado** que o produto já foi adicionado  
**Quando** tenta adicionar novamente  
**Então** deve impedir duplicação ou alterar para "Remove"

---

## 4.  Remover Produtos do Carrinho

### Cenário: Remover produto
**Dado** que o produto está no carrinho  
**Quando** o usuário clica em "Remove"  
**Então** o produto deve ser removido  
E o contador atualizado

---

### Cenário: Carrinho vazio
**Dado** que não há produtos no carrinho  
**Então** o ícone não deve exibir número

---

## 5.  Acesso ao Carrinho

### Cenário: Abrir carrinho
**Dado** que existem produtos no carrinho  
**Quando** o usuário clica no ícone  
**Então** deve ser redirecionado para a página do carrinho

---

## 6.  Ordenação de Produtos

### Cenário: Nome A-Z
**Quando** seleciona "Name (A to Z)"  
**Então** produtos aparecem em ordem crescente

### Cenário: Nome Z-A
**Quando** seleciona "Name (Z to A)"  
**Então** produtos aparecem em ordem decrescente

### Cenário: Preço crescente
**Quando** seleciona "Price low to high"  
**Então** produtos aparecem do menor para o maior preço

### Cenário: Preço decrescente
**Quando** seleciona "Price high to low"  
**Então** produtos aparecem do maior para o menor preço

---

## 7. Layout Responsivo

### Cenário: Visualização em mobile
**Dado** que o usuário usa um dispositivo móvel  
**Então**:
- Layout deve se adaptar à tela
- Botões devem continuar clicáveis

---

## 8. Persistência de Estado

### Cenário: Manter carrinho após refresh
**Dado** que há produtos no carrinho  
**Quando** a página é atualizada  
**Então** os produtos permanecem no carrinho

---

### Cenário: Menu lateral
**Dado** que clico no menu lateral
**Quando** o menu lateral é aberto  
**Então** todos os itens devem funcionar corretamente

#  BUG 02 DO DOC – Expiração Inesperada de Sessão

##  Título
Sessão expira com frequência na página de login, impedindo autenticação consistente

---

##  Ambiente de Teste
- **Plataforma:** Swag Labs  
- **URL:** https://saucedemo.com  
- **Navegador:** Chrome  
- **Dispositivo:** Desktop  

---

##  Descrição
A sessão do usuário expira ou é invalidada de forma prematura após o login.

Mesmo utilizando credenciais válidas, o sistema encerra a sessão e redireciona o usuário para a página de login com erro.

---

##  Passos para Reproduzir
1. Acessar a página de login  
2. Inserir username e password válidos  
3. Realizar login com sucesso  
4. Aguardar alguns minutos na homepage  
5. Atualizar a página ou interagir com o sistema  

---

##  Resultado Atual
- Usuário é redirecionado para a página de login  
- Mensagem exibida:

> Epic sadface: You can only access 'inventory.html' when you are logged in.

- Sessão é encerrada automaticamente após curto período de inatividade  

---

##  Resultado Esperado
- Usuário deve permanecer autenticado por um período normal de sessão  
- A sessão não deve expirar rapidamente sem ação do usuário  
- Navegação entre páginas deve ser estável  

---

##  Impacto
- Bloqueia fluxo de compra  
- Impede execução de testes funcionais completos  
- Afeta diretamente o fluxo principal (login → navegação → compra)  

---

##  Severidade
Alta

---

##  Possíveis Causas (Hipóteses)
- Token de sessão expirando prematuramente  
- Problema no gerenciamento de cookies ou local storage  
- Timeout de sessão configurado incorretamente  
