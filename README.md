Aqui está o **README do jeito que você falaria**, claro, direto, didático, com explicações completas para registro de entendimento — como se fosse você preparando o material da aula para seus alunos e para o time.

---

# 📘 Fluxo de Trabalho com Git e GitHub em Time

### (GitFlow manual — tudo explicado para registro de entendimento)

Este documento é o meu **guia oficial de trabalho em equipe usando Git e GitHub**, baseado no modelo GitFlow, **mas sem usar os comandos automáticos do git-flow**.
Aqui eu explico tudo do jeito que eu entendo e que quero que vocês entendam também: onde cada branch entra, por que fazemos desse jeito e todos os comandos que realmente vamos usar no dia a dia.

A ideia é simples: **organizar o desenvolvimento, evitar bagunça, facilitar correções e manter o código limpo e versionado**.

---

# 1. Por que usamos esse fluxo

Eu sigo o GitFlow porque ele **organiza o projeto**, principalmente quando várias pessoas mexem no código ao mesmo tempo.
Assim, cada um sabe exatamente onde criar sua funcionalidade, onde corrigir problema urgente e qual caminho o código percorre até chegar na produção.

### Por que isso é bom:

* Evita conflito desnecessário
* Mantém histórico limpo
* Torna revisão mais fácil
* Separa claramente ambiente de produção do ambiente de desenvolvimento
* Todo mundo trabalha alinhado

---

# 2. Estrutura das branches e o que cada uma significa

Quero que vocês fixem isso muito bem, porque a base de tudo é **entender o papel de cada branch**.

### `main`

É o **código que está em produção**.
Tudo o que está aqui precisa funcionar. Não se programa diretamente nela.

### `develop`

É onde a gente integra as funcionalidades antes de preparar uma versão.
É o nosso “pré-produção”.

### `feature/*`

Aqui criamos funcionalidades novas.
Exemplos:

* `feature/login`
* `feature/tela-cadastro`

Sempre nasce a partir de `develop`.
Quando termina → PR para `develop`.

### `release/*`

Quando juntamos um lote de funcionalidades e queremos preparar uma nova versão da aplicação.
Exemplo: `release/v1.2.0`.

### `hotfix/*`

Correções urgentes que precisam ir direto para produção.
Essas nascem a partir da `main`.

---

# 3. Comandos essenciais explicados como eu ensino

### 1) Clonar o repositório

```bash
git clone <url>
cd <nome-do-projeto>
```

Baixa tudo para sua máquina. Só faz isso na primeira vez.

---

## Criando a branch develop (se ainda não existir)

```bash
git checkout -b develop
git push -u origin develop
```

`-u` serve para vincular sua branch local à remota.

---

# 4. Fluxo completo de uma Feature (meu passo a passo)

### 1. Atualiza seu develop antes de tudo

```bash
git checkout develop
git pull origin develop
```

Isso evita conflito desnecessário.

### 2. Cria a branch da feature

```bash
git checkout -b feature/nome-da-feature
```

### 3. Programa normalmente

Vai alterando os arquivos e testando.

### 4. Adiciona e faz commit

```bash
git add .
git commit -m "feat: descrição da funcionalidade"
```

### 5. Envia a branch para o GitHub

```bash
git push -u origin feature/nome-da-feature
```

### 6. Abre o Pull Request

Destino sempre: **develop**.

Depois que aprovar → merge → apagar branch.

---

# 5. Fluxo de Release (quando vamos preparar uma nova versão)

### 1. Atualiza develop

```bash
git checkout develop
git pull origin develop
```

### 2. Cria a branch de release

```bash
git checkout -b release/v1.0.0
```

### 3. Ajusta o que for necessário

Changelog, pequenas correções, versão, etc.

### 4. Envia pro GitHub

```bash
git push -u origin release/v1.0.0
```

### 5. PR para a main

Depois do merge:

### 6. Cria a tag da versão

```bash
git checkout main
git pull origin main
git tag -a v1.0.0 -m "Release v1.0.0"
git push origin v1.0.0
```

### 7. Mescla a main de volta no develop

```bash
git checkout develop
git merge main
git push origin develop
```

---

# 6. Fluxo de Hotfix (problema urgente em produção)

Quando tem erro que precisa corrigir rápido:

### 1. Criar branch a partir da main

```bash
git checkout main
git pull origin main
git checkout -b hotfix/corrige-bug-x
```

### 2. Corrigir + commit

```bash
git add .
git commit -m "fix: correção urgente X"
git push -u origin hotfix/corrige-bug-x
```

### 3. Abrir PR para main

Após merge:

### 4. Criar tag

```bash
git tag -a v1.0.1 -m "Hotfix"
git push origin v1.0.1
```

### 5. Mesclar hotfix em develop

```bash
git checkout develop
git merge main
git push origin develop
```

---

# 7. Commit do jeito certo (como eu ensino)

Eu sigo **Conventional Commits**, que deixa o histórico limpo e organizado:

* `feat:` nova funcionalidade
* `fix:` correção
* `docs:` documentação
* `refactor:` melhoria interna
* `chore:` rotina do projeto

Exemplo bom:

```bash
git commit -m "feat(auth): adiciona login com Google"
```

---

# 8. Comandos extras que eu uso no dia a dia

```bash
git status
```

Mostra o que mudou.

```bash
git log --oneline --graph --decorate --all
```

Histórico visual.

```bash
git fetch
```

Atualiza referências do remoto sem mexer no seu código.

```bash
git pull
```

Traz e mescla.

```bash
git stash
```

Guarda alterações sem commitar.

```bash
git branch -d nome
git push origin --delete nome
```

Deletar branch local/remota.

---

# 9. Conflitos – como eu explico

Conflito acontece quando duas pessoas mexem na mesma linha.
O Git marca assim:

```
<<<<<<< HEAD
seu código
=======
código da outra branch
>>>>>>> develop
```

Você escolhe o que fica, ajusta, salva:

```bash
git add arquivo
git commit
```

---

# 10. Meu roteiro de aula usando esse README

1. Apresento teoria rápida das branches
2. Demostro criação de feature
3. Cada aluno cria a própria
4. Fazem commit, push e PR
5. Revisam PR dos colegas
6. Depois faço release ao vivo
7. Por fim, simulo um hotfix

---

# 11. Checklist final (para ver se aprendeu mesmo)

* [ ] Sei o papel de cada branch (main, develop, feature, release, hotfix)
* [ ] Sei criar uma feature e abrir PR
* [ ] Sei atualizar a branch antes de trabalhar
* [ ] Sei fazer release com tag
* [ ] Sei criar hotfix
* [ ] Sei resolver conflito

