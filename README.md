
# 📁 Git - Controle de Versão

## 📌 O que é o Git?

O **Git** é um sistema de controle de versão distribuído, usado para rastrear mudanças no código-fonte durante o desenvolvimento de software. Ele permite que equipes trabalhem simultaneamente em projetos, mantendo um histórico de alterações, facilitando o versionamento, a colaboração e a reversão de mudanças quando necessário.

> Criado por Linus Torvalds (criador do Linux), o Git é hoje a principal ferramenta de versionamento utilizada por desenvolvedores no mundo todo.

## 🚀 Por que usar o Git?

- Histórico de versões de código.
- Trabalhar em equipe de forma eficiente.
- Possibilidade de ramificação (branches) para desenvolvimento de novas funcionalidades sem afetar o código principal.
- Integração com plataformas como GitHub, GitLab e Bitbucket.

## 🧠 Conceitos Fundamentais do Git

### 📁 Repositórios
Um repositório Git é onde o Git armazena todos os arquivos do projeto, é como um **diretório de arquivos e pastas** que possui um **histórico de todas as alterações (log)**, suporta criação de **branches (ramos)** e **merging (mesclagem)** e permite **reversão de alterações**. Existem dois tipos:

 - **Repositório local:** É o repositório na sua máquina. Você trabalha localmente com commits, branches, etc.

 - **Repositório remoto:** É uma cópia hospedada em um servidor (como o GitHub, GitLab ou Bitbucket) usada para compartilhar o código com outras pessoas.

### 📝 Commits
Um commit é como uma fotografia do estado atual do seu código. Cada commit salva as mudanças feitas desde o último commit. Ele contém:

 - Registro de alterações
 - Mensagem de explicação sobre o que foi alterado
 - Identificação única
 - Ratreabilidade (Identifica quem fez, o quê fez e quando fez)
 - Reversão (Reverter alterações em ordem conológica)
 - Base para colaboração (Cada desenvolvedor faz a sua alterações de forma organizada e paralela)

 ### 🔄 Estados de Alteração
O Git trabalha com três principais áreas e quatro estados possíveis para os arquivos:

1. **Untracked (Não rastreado):** Arquivos que existem na pasta do projeto, mas que o Git ainda não está monitorando.

2. **Unmodified (Não modificado):** Arquivos que o Git está rastreando e que não foram alterados desde o último commit.

3. **Modified (Modificado):** Arquivos rastreados que foram alterados, mas ainda não estão prontos para serem commitados.

4. **Staged (Preparado):** Arquivos modificados que foram adicionados à área de staging e estão prontos para entrar no próximo commit.

### 🌿 Branches
Uma branching (ramificação) é como criar uma linha do tempo alternativa, onde permite que você trabalhe em uma versão isolada do seu projeto e desenvolver funcionalidades e corrigir bugs sem interferir na linha do principal (main/master).

```bash
git branch nova-feature        # Cria a branch
git checkout nova-feature      # Troca para ela
git switch nova-feature        # Alternativa moderna ao checkout
```
### 🔀 Merge
O merge combina as alterações de uma branch com outra. Por exemplo, você pode juntar a branch `nova-feature` com a `main` depois de terminar uma funcionalidade. O pocesso de juntar esses ramos é o que chamamos de merge.

```bash
git checkout main        # Vai para a branch principal
git merge nova-feature   # Mescla as mudanças
```

### ❌ Merge Conflict
Merge Conflict (conflito de mesclagem) ocorre quando você tenta fazer merge entre dois branches que tem alterações conflitantes no mesmo trecho de código.

 - Previne perda de alteração de código
 - Força a revisão manual por um desenvolvedor
 - Destaca apenas trechos em conflito
 - Fornece meio para resolver o conflito de forma simples.

### 📚 Boas Práticas
- O nome da branch deve referenciar seu objetivo
- Faça commmits graduais com descrições claras
- Cada Pull request deve ser o mais granular possível
- Não seja defensivo durante um Code Review
- Prefira fazer Pair Programming sempre que possível

### 🌲 As Três Arvores de Trabalho
- **HEAD:** Aponta para o último commit da branch atual
- **Index:** Área de preparação do próximo commit (Stage)
- **Working Directory (Working Tree):** Diretório raiz do seu projeto

## 🛠️ Principais Comandos do Git

### 🔧 Configuração Inicial

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seuemail@exemplo.com"
```

### 📂 Inicializar um repositório

```bash
git init
```

### 📥 Clonar um repositório remoto

```bash
git clone <url-do-repositorio>
```

### 📄 Verificar status do repositório

```bash
git status
```

### ➕ Adicionar arquivos à área de staging

```bash
git add <arquivo>
git add .  # Adiciona todos os arquivos alterados
```

### 💾 Criar um commit

```bash
git commit -m "Mensagem descritiva"
```

### 🔁 Ver histórico de commits

```bash
git log
```

### 🔄 Enviar alterações para o repositório remoto

```bash
git push origin <nome-da-branch>
git push --set-upstream origin <nome-da-branch> # Caso a branch não exista em seu repositório remoto
```

### ⬇️ Baixar alterações do repositório remoto

```bash
git pull
```

### 🌿 Criar e trocar de branch

```bash
git branch nome-da-branch
git checkout nome-da-branch
git switch nome-da-branch
```

### 🧳 Guardando alterações temporariamente
O `git stash` é usado para salvar modificações locais não commitadas (em tracked files) de forma temporária, "limpando" seu diretório de trabalho para que você possa trocar de branch ou trabalhar em outra tarefa.

```bash
git stash # Aplicar as alterações (mais recente) sem removê-las do stash
git stash list # listar os stashes salvos
git stash apply stash@{2} # Aplicar um stash específico
git stash branch nova-branch stash@{0} # Criar uma nova branch a partir de um stash
git stash pop stash@{0} # Aplicar as alterações removendo do stash
```
### 🧹 Remover arquivos não rastreados
O `git clean` é usado para deletar arquivos e diretórios não rastreados pelo Git — ou seja, que nunca foram adicionados com `git add`.

⚠️ **Cuidado:** Esse comando deleta arquivos para sempre, sem mover para o stash ou lixeira.

```bash
git clean -n # Ver o que será apagado (modo seguro)
git clean -f # Remover arquivos não rastreados
git clean -fd # Remover arquivos e diretórios não rastreados
git clean -f -d  # Limpar apenas diretórios
```

### 🔀 Mesclar branches (Merge vs. Rebase)

#### 🧩 O que é git merge?
O comando git merge combina o histórico de duas branches, criando um novo commit de merge quando necessário. Ele preserva o histórico como ele realmente aconteceu — com todos os commits e bifurcações.

**Exemplo:**
```bash
git checkout main
git merge nome-da-branch
```
📌 O Git cria um commit especial (merge commit) caso a branch tenha commits únicos. O histórico fica "ramificado", mostrando visualmente que as branches se uniram.

##### ✔️ Vantagens do Merge:
- Mantém o histórico completo e fiel da colaboração.
- Ideal para equipes trabalhando simultaneamente em diferentes branches.

##### ⚠️ Desvantagem:
- O histórico pode ficar poluído com muitos commits de merge, dificultando a leitura.

##### 🤔 Características do Merge
- Cria-se um **novo** merge commit
- Esse commit possui **duas** origens
- É difícil de **reverter** um merge commit (reverte o histórico)
- **Ideal** para trabalho em **time** na mesma branch

#### 🏃🏼‍➡️ Passo a Passo do Merge

**1. Estado atual**
<div>
  <img src="https://raw.githubusercontent.com/Willian-Brito/git-learning/refs/heads/master/prints/Merge%20-%20passo1.png"/>
</div>

**2. Cria o merge commit**
<div>
  <img src="https://raw.githubusercontent.com/Willian-Brito/git-learning/refs/heads/master/prints/Merge%20-%20passo2.png"/>
</div>

**3. Aponta para os últimos commits das branchs origem/destino**
<div>
  <img src="https://raw.githubusercontent.com/Willian-Brito/git-learning/refs/heads/master/prints/Merge%20-%20passo3.png"/>
</div>

#### 🔄 O que é git rebase?
O comando git rebase pega os commits de uma branch e "reaplica" eles sobre outra branch, criando um histórico linear.

**Exemplo:**
```bash
git checkout nova-feature
git rebase main
```

📌 Isso "muda a base" da branch nova-feature, como se ela tivesse começado a partir da main, reaplicando seus commits um por um.

##### ✔️ Vantagens do Rebase:
- Cria um histórico linear e limpo, facilitando a leitura e o debug.
- Útil antes de enviar a branch para o repositório remoto, para “limpar” o histórico.

##### ⚠️ Desvantagem:
- Pode causar conflitos difíceis de resolver em branches grandes.
- Não deve ser usado em branches compartilhadas, pois altera o histórico (os hashes dos commits mudam).

##### 🤔 Características do Rebase
- Organiza os commits de forma **linear**
- **Reescreve** o log criando **novos** commits
- Histórico mais **limpo** e alinhado
- **Difícil** de trabalhar de trabalhar em **time** na mesa branch

#### 🏃🏼‍➡️ Passo a Passo do Rebase

**1. Estado atual**
<div>
  <img src="https://raw.githubusercontent.com/Willian-Brito/git-learning/refs/heads/master/prints/Merge%20-%20passo1.png"/>
</div>

**2. Reaponta o histórico de commits para o último commit da branch destino**
<div>
  <img src="https://raw.githubusercontent.com/Willian-Brito/git-learning/refs/heads/master/prints/Rebase%20-%20passo1.png"/>
</div>

**3. Atualiza a HEAD e o histórico passa a fazer parte da branch destino**
<div>
  <img src="https://raw.githubusercontent.com/Willian-Brito/git-learning/refs/heads/master/prints/Rebase%20-%20passo2.png"/>
</div>

#### 🆚 Diferença entre `merge` e `rebase`

| Característica           | `git merge`                          | `git rebase`                         |
|--------------------------|---------------------------------------|---------------------------------------|
| Histórico                | Preserva com bifurcações              | Reescreve para parecer linear         |
| Commit de merge          | Sim                                   | Não                                   |
| Clareza do histórico     | Pode ficar poluído com muitos merges | Histórico mais limpo e sequencial     |
| Segurança                | Seguro em qualquer situação           | Deve ser evitado em branches públicas |
| Ideal para               | Colaboração com múltiplos desenvolvedores | Reorganizar histórico antes de dar push |
| Facilidade de uso        | Mais simples e direto                 | Exige mais cuidado com conflitos      |


### 🚫 Ignorar arquivos

Crie um arquivo `.gitignore` na raiz do projeto:
- Site para gerar gitignore: https://www.toptal.com/developers/gitignore

```bash
node_modules/
.env
*.log
```

### ❌ Reverter mudanças

#### 📌 1. git reset --soft
- Move o HEAD para o commit desejado
- Mantém a área de staging (index) intacta
- Não altera os arquivos no diretório de trabalho

É útil quando você quer reescrever o histórico recente, mas manter as alterações prontas para novo commit.

**Exemplo:**
```bash
git reset --soft HEAD~1 # Volta para o commit anterior mechendo o ponteiro do HEAD
```
✅ **Efeito:** Desfaz o último commit, mas mantém as mudanças na área de staging.

#### 📌 2. git reset --mixed (padrão)
- Move o HEAD para o commit desejado
- Limpa a área de staging
- Não altera os arquivos no diretório de trabalho

É a opção padrão se você usar apenas git reset. Ideal para desfazer um commit e preparar o ambiente para um novo commit com alterações diferentes.

**Exemplo:**
```bash
git reset --mixed HEAD~1
```
✅ **Efeito:** Desfaz o último commit e remove os arquivos da área de staging, mas mantém as mudanças no código (você pode editá-las ou adicioná-las novamente com git add).

#### 📌 3. git reset --hard
Move o HEAD para o commit desejado

Limpa a área de staging

Descarta as alterações no diretório de trabalho

É a opção mais destrutiva. Use com cuidado, pois você perderá quaisquer alterações locais que não tenham sido commitadas.

**Exemplo:**
```bash
git reset --hard HEAD~1
```
❗ **Efeito:** Desfaz o commit, limpa a staging area e remove as alterações feitas nos arquivos – como se nunca tivessem existido.

## 🌐 Integração com GitHub

```bash
git remote add origin https://github.com/usuario/repositorio.git
git push -u origin main
```

## 🪝 Git Hooks
Git Hooks são scripts que o Git executa automaticamente em eventos específicos, como antes de um commit ou após um push. Eles são ideais para automações como:

- Validações antes de um commit
- Formatadores de código
- Execução de testes
- Integrações com ferramentas de CI/CD
- Diretório `.git/hooks`

## 🔖 Git Tagging
Tags servem para marcar pontos importantes no histórico, como releases (v1.0.0, por exemplo).

### ✅ Criar uma tag leve:

```bash
git tag v1.0.0
```

### 📝 Criar uma tag anotada (com mensagem e metadados):
```bash
git tag -a v1.0.0 -m "Primeira versão estável"
```

### 📤 Enviar tags para o repositório remoto:
```bash
git push origin v1.0.0
git push --tags # Enviar todas as tags
```

### 🔍 Ver todas as tags:
```bash
git tag
```

## 📦 Git Submodules
Submodules permitem incluir outro repositório Git dentro de um repositório principal, útil para projetos que compartilham bibliotecas ou módulos reutilizáveis.

### ➕ Adicionar um submódulo:
```bash
git submodule add https://github.com/usuario/projeto-biblioteca libs/biblioteca
```
**Isso:**
- Clona o repositório dentro do diretório libs/biblioteca
- Cria um arquivo .gitmodules para registrar a referência

### 📥 Clonar repositório com submódulos:
```bash
git clone https://github.com/usuario/projeto-principal.git --recurse-submodules # Clona, Inicia e Atualiza submodules
```
**Ou:**
```bash
git clone https://github.com/usuario/projeto-principal.git # Clona submodule
git submodule init # Inicia submodule
git submodule update # Atualiza submodule
```

### 🔄 Atualizar submódulo para a última versão da branch remota:
```bash
cd libs/biblioteca
git checkout main
git pull
cd ../..
```

## 🧬 Git LFS (Large File Storage)
Git LFS é uma extensão para o Git que permite versionar arquivos grandes (como imagens, vídeos, modelos, binários) de forma eficiente, sem comprometer o desempenho do repositório.

### 🧠 Por que usar?
O Git foi projetado para versionar código-fonte e arquivos de texto, e não lida bem com arquivos binários grandes ou frequentemente alterados. O Git LFS resolve isso ao:

- Armazenar referências no Git (um ponteiro pequeno)
- Armazenar o conteúdo real em um repositório remoto separado

### 🔧 Como usar?

```bash
 # 1. Instale o Git LFS:
git lfs install

# 2. Adicione arquivos ao controle do LFS (Isso cria ou atualiza um arquivo .gitattributes):
git lfs track "*.psd" 

# 3. Adicione os arquivos normalmente:
git add arquivo.psd
git commit -m "Adiciona arquivo grande com Git LFS"
git push
```
⚠️ Requer que o repositório remoto também tenha suporte ao Git LFS (como GitHub, GitLab, Bitbucket).

## 📦 Git Bundle (Bundling)
**Git Bundling** permite empacotar todo o histórico de um repositório Git em um único arquivo `.bundle`, útil para:

- Backup
- Transferência via pen drive ou rede offline
- Envio de código onde não é possível usar `git push`

### 📁 Como criar um bundle
```bash
git bundle create meu-repo.bundle --all
```
- Isso gera um arquivo meu-repo.bundle com todo o histórico e branches do repositório.
- Você também pode limitar a um branch:

```bash
git bundle create meu-repo.bundle main
```

### 📥 Como clonar a partir de um bundle
```bash
git clone meu-repo.bundle -b main novo-diretorio
```
- Você pode usar esse bundle como uma origem remota temporária:

```bash
git remote add offline ../meu-repo.bundle
git fetch offline
```

## 🍒 Git Cherry Pick
O comando `git cherry-pick` permite aplicar commits específicos de outra branch à branch atual, sem fazer merge completo. É como escolher “a dedo” (daí o nome cherry-pick) quais commits você quer trazer de uma branch para outra.

### ✅ Quando usar?
- Quando você quer aplicar um bugfix específico feito em outra branch.
- Quando várias features estão em desenvolvimento, mas você só quer trazer uma para a main (sem trazer o restante).
- Para reutilizar commits isolados sem fazer merge de branches inteiras.

#### 📌 Exemplo básico
Suponha que você está na branch main, e quer aplicar um commit que está na branch feature-x.

**1. Liste os commits da branch `feature-x`:**

```bash
git log feature-x
```
**Você verá algo assim:**
```bash
commit a1b2c3d4 - Corrige problema de login
commit e5f6g7h8 - Adiciona botão
```

**2. Aplique o commit na sua branch atual `main`:**
```bash
git cherry-pick a1b2c3d4 # Isso cria um novo commit na sua branch com o mesmo conteúdo daquele commit.
```

### 🔀 Cherry-pick de múltiplos commits
```bash
git cherry-pick commit1 commit2
```
**Ou um intervalo:**
```bash
git cherry-pick a1b2c3d4^..e5f6g7h8 # O ^ indica o commit anterior ao primeiro da sequência.
```

### ⚠️ Possíveis conflitos
- Se houver conflitos durante o cherry-pick, o Git irá pausá-lo e pedir para você resolvê-los manualmente.
- Após resolver os conflitos:
```bash
git add .
git cherry-pick --continue
```

**Se quiser cancelar:**
```bash
git cherry-pick --abort
```

## ✅ Conclusão

O Git é uma ferramenta essencial para qualquer desenvolvedor moderno. Dominar seus comandos básicos é o primeiro passo para trabalhar com segurança e eficiência em projetos colaborativos.
