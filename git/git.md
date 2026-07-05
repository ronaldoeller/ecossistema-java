# Referência Git

Principais comandos com exemplos · Integração com GitHub · Feature Branch Workflow

## Configuração e Inicialização

### `git init`
Inicializa um repositório Git no diretório atual.

```bash
git init
git init meu-projeto
```
*Categoria: Setup*

### `git config`
Define nome e e-mail do usuário (globalmente).

```bash
git config --global user.name "Ana Silva"
git config --global user.email "ana@email.com"
```
*Categoria: Setup*

### `git clone`
Clona um repositório remoto para a máquina local.

```bash
git clone https://github.com/usuario/repo.git
```
*Categoria: Remoto*

## Staging e Commits

### `git status`
Exibe o estado atual do repositório.

```bash
git status
```
*Categoria: Info*

### `git add`
Adiciona arquivo(s) à área de staging.

```bash
git add index.html   # arquivo específico
git add .             # todos os arquivos
```
*Categoria: Stage*

### `git commit`
Registra as mudanças em staging com mensagem descritiva.

```bash
git commit -m "feat: adiciona página de login"
```
*Categoria: Stage*

### `git diff`
Mostra diferenças entre arquivos modificados e o último commit.

```bash
git diff
git diff --staged   # diferenças em staging
```
*Categoria: Info*

## Branches

### `git branch`
Lista, cria ou deleta branches.

```bash
git branch
git branch feature/login
git branch -d feature/login
```
*Categoria: Branch*

### `git checkout` / `git switch`
Troca para outra branch (ou cria e troca).

```bash
git switch feature/login
git switch -c feature/nova   # cria e troca
```
*Categoria: Branch*

### `git merge`
Integra o histórico de outra branch na branch atual.

```bash
git switch main
git merge feature/login
```
*Categoria: Branch*

### `git rebase`
Reaplica commits sobre outra branch, linearizando o histórico.

```bash
git switch feature/login
git rebase main
```
*Categoria: Branch*

## Integração com GitHub (Remoto)

### `git remote`
Gerencia conexões com repositórios remotos.

```bash
git remote add origin https://github.com/user/repo.git
git remote -v   # lista remotos
```
*Categoria: Remoto*

### `git push`
Envia commits locais para o repositório remoto.

```bash
git push origin main
git push -u origin feature/login   # define upstream
```
*Categoria: Remoto*

### `git pull`
Busca e integra mudanças do remoto na branch atual.

```bash
git pull origin main
```
*Categoria: Remoto*

### `git fetch`
Baixa mudanças do remoto sem integrá-las à branch local.

```bash
git fetch origin
git fetch --all   # todos os remotos
```
*Categoria: Remoto*

### `gh pr create`
Cria um Pull Request no GitHub via CLI (requer GitHub CLI).

```bash
gh pr create --title "Adiciona login" --body "Descrição"
```
*Categoria: GitHub CLI*

### `gh repo clone`
Clona repositório do GitHub com autenticação via CLI.

```bash
gh repo clone usuario/repositorio
```
*Categoria: GitHub CLI*

## Histórico e Inspeção

### `git log`
Exibe o histórico de commits do repositório.

```bash
git log --oneline --graph --all
```
*Categoria: Histórico*

### `git show`
Mostra detalhes de um commit específico.

```bash
git show a3f8c21
```
*Categoria: Histórico*

### `git blame`
Mostra quem modificou cada linha de um arquivo.

```bash
git blame src/app.js
```
*Categoria: Histórico*

## Desfazer e Corrigir

### `git restore`
Descarta alterações em arquivos não commitados.

```bash
git restore index.html
git restore --staged index.html   # retira do staging
```
*Categoria: Desfazer*

### `git revert`
Cria um novo commit que desfaz as mudanças de um commit anterior.

```bash
git revert a3f8c21
```
*Categoria: Desfazer*

### `git reset`
Move o HEAD para um commit anterior. Use com cautela.

```bash
git reset --soft HEAD~1   # mantém staged
git reset --hard HEAD~1   # descarta tudo
```
*Categoria: Desfazer*

### `git stash`
Salva temporariamente mudanças não commitadas.

```bash
git stash
git stash pop   # restaura o último stash
```
*Categoria: Desfazer*

## Tags e Cherry-pick

### `git tag`
Cria marcações em commits específicos (ex: versões de release).

```bash
git tag v1.0.0
git tag -a v1.0.0 -m "Release 1.0"
git push origin v1.0.0   # envia tag ao GitHub
```
*Categoria: Tags*

### `git cherry-pick`
Aplica um commit específico de outra branch na branch atual.

```bash
git cherry-pick a3f8c21
```
*Categoria: Branch*

---

## Feature Branch Workflow

Fluxo de trabalho típico para desenvolvimento em equipe com Git e GitHub.

### 1. Criar uma branch para a nova feature
Nunca desenvolva diretamente na main. Crie uma branch com nome descritivo.

```bash
git switch main
git pull origin main
git switch -c feature/login
```

### 2. Desenvolver e commitar incrementalmente
Edite os arquivos. Adicione ao staging e faça commits com mensagens claras. Repita este ciclo quantas vezes precisar.

```bash
git add .
git commit -m "feat: adiciona formulário de login"
```

### 3. Enviar a branch ao GitHub
Publique a branch remota para que outros possam ver e revisar o código.

```bash
git push -u origin feature/login
```

### 4. Abrir um Pull Request (PR)
No GitHub (ou via CLI), abra um PR da sua branch para a main. Descreva as mudanças e solicite revisão da equipe.

```bash
gh pr create --title "feat: login" --body "Adiciona autenticação"
```

### 5. Code Review e ajustes
Responda ao feedback da revisão. Corrija e faça novos commits na mesma branch. O PR é atualizado automaticamente com os novos pushes.

```bash
git commit -m "fix: corrige validação de senha"
git push
```

### 6. Merge do PR no GitHub
Após aprovação, faça o merge do PR na branch main pelo GitHub. O GitHub cria um merge commit ou faz squash, conforme configuração do repositório.

```bash
# Feito via interface do GitHub ou:
gh pr merge --squash
```

### 7. Atualizar o repositório local
Volte para a main local e puxe as alterações recém-mergeadas.

```bash
git switch main
git pull origin main
```

### 8. Deletar a branch usada
Mantenha o repositório limpo removendo a branch que já foi mergeada.

```bash
git branch -d feature/login
git push origin --delete feature/login   # deleta no remoto
```

> **Dica:** Use mensagens de commit no padrão Conventional Commits: `feat:`, `fix:`, `docs:`, `chore:`, `refactor:`. Facilita a geração automática de changelogs e a leitura do histórico.

---

## Exemplo Prático: Sistema de Tarefas

Do zero ao GitHub — criação, evolução e manutenção de um projeto real passo a passo.

### Cenário

Vamos criar do zero um sistema simples de gerenciamento de tarefas em Python (`todo_app`). Ao longo do exemplo, vamos: criar o projeto, versionar no Git, publicar no GitHub, evoluir o código em branches separadas, corrigir um bug e simular o trabalho em equipe com Pull Requests.

### Fase 1 — Criando o projeto e o primeiro commit

**1.1 Criar a estrutura do projeto e inicializar o repositório**

```bash
# Cria a pasta do projeto e entra nela
$ mkdir todo_app && cd todo_app

# Inicializa o repositório Git
$ git init
Initialized empty Git repository in ~/todo_app/.git/

# Configura identidade (se ainda não configurado globalmente)
$ git config user.name "Ana Silva"
$ git config user.email "ana@email.com"
```

**1.2 Criar o arquivo principal da aplicação**

`todo_app/tasks.py`

```python
# tasks.py — Sistema de gerenciamento de tarefas
tasks = []

def add_task(title):
    tasks.append({"title": title, "done": False})
    print(f"Tarefa adicionada: {title}")

def list_tasks():
    if not tasks:
        print("Nenhuma tarefa encontrada.")
        return
    for i, t in enumerate(tasks, 1):
        status = "[x]" if t["done"] else "[ ]"
        print(f"{i}. {status} {t['title']}")

if __name__ == '__main__':
    add_task("Estudar Git")
    add_task("Criar Pull Request")
    list_tasks()
```

**1.3 Criar o `.gitignore` e fazer o primeiro commit**

```bash
# Cria o .gitignore para ignorar arquivos desnecessários
$ echo '__pycache__/' > .gitignore
$ echo '*.pyc' >> .gitignore
$ echo '.env' >> .gitignore

# Verifica o estado do repositório
$ git status
On branch main
Untracked files:
    tasks.py
    .gitignore

# Adiciona todos os arquivos ao staging
$ git add .

# Cria o primeiro commit
$ git commit -m "feat: estrutura inicial do todo_app"
[main (root-commit) a1b2c3d] feat: estrutura inicial do todo_app
 2 files changed, 18 insertions(+)
```

### Fase 2 — Publicando no GitHub

**2.1 Criar o repositório no GitHub e conectar o remoto**

```bash
# Cria o repositório no GitHub via CLI (GitHub CLI)
$ gh repo create todo_app --public --source=. --push
✓ Created repository ana/todo_app on GitHub
✓ Pushed commits to github.com/ana/todo_app

# -- OU -- manualmente, após criar o repo no GitHub:
$ git remote add origin https://github.com/ana/todo_app.git
$ git push -u origin main
Branch 'main' set up to track remote branch 'main' from 'origin'.
To github.com:ana/todo_app.git
   a1b2c3d..  main -> main
```

> **Dica:** A flag `-u` (`--set-upstream`) define o remoto padrão para a branch. Após isso, basta usar `git push` e `git pull` sem precisar especificar `origin main`.

### Fase 3 — Nova feature: concluir tarefas (em branch separada)

**3.1 Criar branch para a nova funcionalidade**

```bash
# Garante que a main está atualizada
$ git switch main
$ git pull origin main

# Cria e troca para a branch da nova feature
$ git switch -c feature/complete-task
Switched to a new branch 'feature/complete-task'
```

**3.2 Adicionar a função `complete_task()` no arquivo**

`todo_app/tasks.py` (trecho adicionado)

```python
def complete_task(index):
    """Marca uma tarefa como concluída pelo índice (1-based)."""
    if index < 1 or index > len(tasks):
        print("Índice inválido.")
        return
    tasks[index - 1]['done'] = True
    print(f"Tarefa {index} concluída!")

if __name__ == '__main__':
    add_task("Estudar Git")
    add_task("Criar Pull Request")
    complete_task(1)  # <-- nova chamada
    list_tasks()
```

**3.3 Commitar e enviar a branch ao GitHub**

```bash
$ git add tasks.py
$ git commit -m "feat: adiciona funcao complete_task"
[feature/complete-task e4f5a6b] feat: adiciona funcao complete_task
 1 file changed, 8 insertions(+)

$ git push -u origin feature/complete-task
Branch 'feature/complete-task' tracking 'origin/feature/complete-task'
```

**3.4 Abrir Pull Request e fazer merge**

```bash
# Abre PR via GitHub CLI
$ gh pr create \
  --title "feat: concluir tarefas" \
  --body "Adiciona complete_task() com validação de índice" \
  --base main
https://github.com/ana/todo_app/pull/1

# Após revisão e aprovação, faz o merge:
$ gh pr merge 1 --squash --delete-branch
✓ Squashed and merged pull request #1
✓ Deleted branch feature/complete-task
```

**3.5 Atualizar a main local após o merge**

```bash
$ git switch main
$ git pull origin main
Updating a1b2c3d..e4f5a6b
Fast-forward
 tasks.py | 8 ++++++++
```

### Fase 4 — Corrigindo um bug em produção

> **Bug:** Um usuário reportou que ao chamar `complete_task(0)` o sistema não exibe mensagem de erro correta. Precisamos corrigir imediatamente na main.

**4.1 Criar branch de hotfix a partir da main**

```bash
$ git switch main
$ git pull origin main
$ git switch -c hotfix/complete-task-validation
```

**4.2 Corrigir a validação e commitar**

`tasks.py` — antes (linha com bug)

```python
# BUG: índice 0 passa na checagem pois 0 < 1 é True,
# mas a mensagem só aparece se index > len(tasks)
if index < 1 or index > len(tasks):
```

`tasks.py` — depois (correção)

```python
# CORREÇÃO: valida explicitamente o intervalo [1, len(tasks)]
if not (1 <= index <= len(tasks)):
    print(f"Erro: índice {index} fora do intervalo válido.")
    return
```

```bash
$ git add tasks.py
$ git commit -m "fix: corrige validacao de indice em complete_task"
[hotfix/complete-task-validation f7g8h9i] fix: corrige validacao...

$ git push -u origin hotfix/complete-task-validation

# PR de emergência e merge direto:
$ gh pr create --title 'fix: validação complete_task' --base main
$ gh pr merge --squash --delete-branch
✓ Merged and deleted hotfix branch
```

### Fase 5 — Outro desenvolvedor contribui ao mesmo tempo

> **Contexto:** O desenvolvedor Bruno está trabalhando em outra feature (remover tarefas) enquanto Ana já fez merge de uma correção. Veja como sincronizar sem conflitos.

**5.1 Bruno cria sua branch e desenvolve**

```bash
# Bruno clona o repositório
$ git clone https://github.com/ana/todo_app.git
$ cd todo_app

# Cria branch para sua feature
$ git switch -c feature/remove-task

# Adiciona a função remove_task() ao tasks.py
$ git add tasks.py
$ git commit -m "feat: adiciona funcao remove_task"
```

**5.2 Enquanto isso, Ana faz merge de hotfix na main. Bruno precisa atualizar sua branch.**

```bash
# Bruno atualiza a referência do remoto
$ git fetch origin
remote: Counting objects: 3, done.
   e4f5a6b..f7g8h9i  main -> origin/main

# Rebaseia a branch de Bruno sobre a main atualizada
$ git rebase origin/main
Successfully rebased and updated refs/heads/feature/remove-task

# Sobe a branch rebaseada (força push pois o histórico mudou)
$ git push --force-with-lease origin feature/remove-task
```

> **Atenção:** `--force-with-lease` é mais seguro que `--force`: só sobrescreve se ninguém mais tiver feito push na branch desde o último fetch.

**5.3 Bruno abre PR e a equipe revisa**

```bash
$ gh pr create --title "feat: remover tarefa" --base main
https://github.com/ana/todo_app/pull/2

# Ana revisa e deixa um comentário no PR via GitHub
# Bruno ajusta e faz novo commit na mesma branch:
$ git commit -m "refactor: trata lista vazia em remove_task"
$ git push

# Após aprovação:
$ gh pr merge 2 --squash --delete-branch
✓ Merged pull request #2
```

### Fase 6 — Inspecionando o histórico do projeto

Após várias contribuições, veja como visualizar e navegar pelo histórico:

```bash
# Histórico visual compacto
$ git log --oneline --graph --all
* j0k1l2m (HEAD -> main, origin/main) feat: remover tarefa
* f7g8h9i fix: corrige validacao de indice em complete_task
* e4f5a6b feat: adiciona funcao complete_task
* a1b2c3d feat: estrutura inicial do todo_app

# Ver o que mudou em um commit específico
$ git show f7g8h9i

# Ver quem alterou cada linha do arquivo
$ git blame tasks.py
f7g8h9i (Ana Silva 2024-06-01) def complete_task(index):
j0k1l2m (Bruno Lima 2024-06-02) def remove_task(index):

# Desfazer último commit mantendo as alterações staged
$ git reset --soft HEAD~1

# Criar tag de release
$ git tag -a v1.0.0 -m "Release 1.0 — CRUD básico de tarefas"
$ git push origin v1.0.0
```

---

## Resumo

Fluxo consolidado:

```
git init → git add / commit → git push → git switch -c → commits na branch →
git push → gh pr create → code review → merge → git pull
```

Repita o ciclo de branch para cada feature ou correção.
