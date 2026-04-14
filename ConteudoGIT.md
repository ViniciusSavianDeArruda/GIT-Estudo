# 📚 Git - Guia de Estudos

Um guia completo sobre Git e controle de versão criado para estudo e para iniciantes e desenvolvedores.

## 📋 Índice

- [Conceitos Básicos](#-conceitos-básicos)
- [Configuração Inicial](#️-configuração-inicial)
- [Ciclo Básico de Trabalho](#️-ciclo-básico-de-trabalho)
- [Trabalhando com Branches](#️-trabalhando-com-branches)
- [Merge e Pull Requests](#️-merge-e-pull-requests)
- [Sincronização com Repositório Remoto](#️-sincronização-com-repositório-remoto)
- [Comandos Úteis](#️-comandos-úteis)
- [Recursos Avançados](#-recursos-avançados)
- [Fluxo de Trabalho Completo](#-fluxo-de-trabalho-completo)
- [Boas Práticas](#-boas-práticas)
- [Tomada de Decisão com Git](#-tomada-de-decisão-com-git)

---

## 🎯 Conceitos Básicos

### Terminologia Essencial

- **Git**: Sistema de controle de versão distribuído
- **Repositório (repo)**: Local onde o Git armazena todos os arquivos do projeto e histórico de alterações
- **Commit**: "Foto" do estado atual do projeto em um momento específico
- **Branch (ramificação)**: Linha de desenvolvimento independente. A principal geralmente é `main` ou `master`
- **Merge**: Juntar alterações de uma branch com outra
- **Pull Request (PR)**: Pedido de integração de uma branch com outra, geralmente no GitHub, com revisão de código

---

## ⚙️ Configuração Inicial

```bash
# Configurar usuário globalmente
git config --global user.name "Seu Nome"
git config --global user.email "email@exemplo.com"

# Verificar configurações
git config --list

# Inicializar um repositório local
git init

# Clonar um repositório remoto
git clone https://github.com/usuario/repositorio.git
```

---

## 🔄 Ciclo Básico de Trabalho

```bash
# Ver status do repositório (arquivos modificados, não adicionados, etc.)
git status

# Adicionar arquivos para commit (staging area)
git add nome_do_arquivo
git add .                    # adiciona todos os arquivos modificados
git add *.js                 # adiciona todos os arquivos .js

# Criar commit
git commit -m "Mensagem descritiva do commit"

# Ver histórico de commits
git log
git log --oneline           # versão resumida
git log --graph             # visualização gráfica
```

### 📊 Fluxo Visual do Ciclo

```
Working Directory → Staging Area → Repository
     (git add)         (git commit)
```

---

## 🌿 Trabalhando com Branches

```bash
# Criar uma nova branch
git branch nome_da_branch

# Listar todas as branches
git branch                  # branches locais
git branch -a              # todas as branches (locais e remotas)

# Trocar de branch
git checkout nome_da_branch

# Criar e já mudar para a branch (comando mais usado)
git checkout -b nome_da_branch

# Comando moderno para trocar de branch
git switch nome_da_branch
git switch -c nome_da_branch  # criar e trocar
```

### 💡 Convenções de Nomenclatura

Sempre use nomes descritivos para suas branches:

- `feature/login` - nova funcionalidade
- `feature/user-dashboard` - painel do usuário
- `bugfix/navbar-responsive` - correção de bug
- `hotfix/security-patch` - correção urgente

---

## 🔀 Merge e Pull Requests

### Merge Local

```bash
# Estando na branch principal, juntar outra branch
git checkout main
git merge nome_da_branch

# Em caso de conflitos, resolver manualmente e depois:
git add .
git commit -m "Resolve conflitos do merge"
```

### Pull Request no GitHub

1. **Faça push da sua branch:**
   ```bash
   git push -u origin nome_da_branch
   ```

2. **No GitHub:**
   - Vá para o repositório
   - Clique em "Compare & pull request"
   - Adicione título e descrição
   - Criar pull request

3. **Revisão e Aprovação:**
   - Outros desenvolvedores revisam o código
   - Fazem comentários e sugestões
   - Aprovam as mudanças
   - Fazem o merge

---

## 🔄 Sincronização com Repositório Remoto

```bash
# Enviar commits para o repositório remoto
git push                              # se já configurado
git push -u origin nome_da_branch     # primeira vez

# Baixar alterações do remoto
git pull                              # baixa e faz merge automaticamente
git fetch                             # apenas baixa, sem fazer merge

# Ver repositórios remotos configurados
git remote -v

# Adicionar repositório remoto
git remote add origin https://github.com/usuario/repo.git
```

---

## 🛠️ Comandos Úteis

### Visualização e Comparação

```bash
# Ver diferenças antes do commit
git diff                              # diferenças não staged
git diff --staged                     # diferenças staged
git diff branch1 branch2              # comparar branches

# Ver detalhes de um commit específico
git show <hash_do_commit>
```

### Desfazer Alterações

```bash
# Cancelar alterações locais (não commitadas)
git restore nome_do_arquivo           # comando moderno
git checkout -- nome_do_arquivo       # comando antigo

# Remover arquivo da staging area
git restore --staged nome_do_arquivo

# Reverter um commit já feito (cria novo commit)
git revert <hash_do_commit>

# Voltar para um commit específico (CUIDADO!)
git reset --hard <hash_do_commit>
```

### Limpeza

```bash
# Apagar branch local
git branch -d nome_da_branch          # apenas se já foi merged
git branch -D nome_da_branch          # força a exclusão

# Apagar branch remota
git push origin --delete nome_da_branch

# Limpar branches que não existem mais no remoto
git remote prune origin
```

---
## 🧠 Recursos Avançados

### 📦 Stash (Trabalho Temporário)

```bash
git stash
git stash list
git stash apply
git stash drop
git stash clear
```

### Rebase
```bash
  git rebase main
```

 - 💡 Reorganiza o histórico de commits de forma linear.

 - ⚠️ Evite usar em branches já compartilhadas.

### 🍒 Cherry-pick
```bash
git cherry-pick <hash>
```

💡 Aplica um commit específico em outra branch.

### 🚫 .gitignore

Arquivo que define o que não deve ser versionado.

Exemplo:
```
node_modules/
.env
dist/
*.log
```
---

## 🚀 Fluxo de Trabalho Completo

### Exemplo Prático: Desenvolvendo uma Nova Feature

```bash
# 1. Atualizar branch principal
git checkout main
git pull

# 2. Criar nova branch para a feature
git checkout -b feature/sistema-login

# 3. Fazer alterações e commits
# ... editar arquivos ...
git add .
git commit -m "Adiciona formulário de login"

# ... mais alterações ...
git add .
git commit -m "Implementa validação de email"

# 4. Enviar branch para o remoto
git push -u origin feature/sistema-login

# 5. Abrir Pull Request no GitHub
# (feito pela interface web)

# 6. Após aprovação e merge, limpar
git checkout main
git pull
git branch -d feature/sistema-login
```

---

## ✨ Boas Práticas

### 🏷️ Nomenclatura de Branches

- ✅ **Bom**: `feature/user-authentication`, `bugfix/navbar-mobile`
- ❌ **Ruim**: `nova`, `teste`, `branch1`

### 📝 Mensagens de Commit

- ✅ **Bom**: `"Corrige validação de email no formulário de login"`
- ❌ **Ruim**: `"fix"`, `"mudanças"`, `"wip"`

### 🔄 Fluxo de Desenvolvimento

1. **Sempre trabalhe em branches separadas** - nunca diretamente na `main`
2. **Faça commits pequenos e frequentes** - facilita revisão e rollback
3. **Atualize sua branch regularmente**:
   ```bash
   git checkout main
   git pull
   git checkout minha-branch
   git merge main  # ou git rebase main
   ```
4. **Use Pull Requests** - garantem revisão de código e qualidade
5. **Limpe branches antigas** - mantenha o repositório organizado

### 🚨 Resolução de Conflitos

Conflitos são normais! Quando acontecem:

1. Git marca os arquivos conflitantes
2. Abra os arquivos e procure por:
   ```
   <<<<<<< HEAD
   seu código
   =======
   código conflitante
   >>>>>>> branch-name
   ```
3. Escolha qual versão manter (ou combine ambas)
4. Remova as marcações do Git
5. Faça commit da resolução

### 🧩 Estratégias de Branching

#### GitHub Flow
- main sempre estável
- tudo via Pull Request

#### Git Flow
- main → produção
- develop → desenvolvimento
- feature/* → funcionalidades
- hotfix/* → correções urgentes

💡 Escolha depende do tamanho do projeto.

---

## 🧠 Tomada de Decisão com Git

### Merge vs Rebase

- **Merge**
  - Mantém histórico completo
  - Mais seguro para equipes

- **Rebase**
  - Histórico linear
  - Mais limpo visualmente

💡 Regra prática:
- Use **merge** em colaboração
- Use **rebase** localmente para organizar commits

## 📚 Recursos Adicionais

- [Documentação Oficial do Git](https://git-scm.com/doc)
- [GitHub Guides](https://guides.github.com/)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)

---

## 🤝 Contribuindo

Este é um guia de estudos. Sinta-se à vontade para sugerir melhorias através de Pull Requests!

---
