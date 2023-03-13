## Instalar o Git no Windows

### Instalador autônomo do Git para Windows

1. Baixe o instalador mais recente do [Git for Windows](https://git-for-windows.github.io/).

2. Quando você tiver iniciado o instalador com sucesso, vai ver a tela do assistente de **configuração do Git**. Siga os avisos **Next** e **Finish** para concluir a instalação. As opções padrão são bastante sensíveis para a maioria dos usuários.

3. Abra um prompt de comando (ou Git Bash se durante a instalação você optou por não usar o Git do Prompt de Comando do Windows).

4. Execute os comandos a seguir para configurar o nome do usuário e e-mail do Git, substituindo o nome Emma pelo seu próprio. Essas informações vão ser associadas a quaisquer commits que você criar:

   ```js
    $ git config --global user.name "Emma Paris" $ git config --global user.email "eparis@atlassian.com"
   ```

5. *Opcional: instale o auxiliar de credenciais do Git no Windows*

   O Bitbucket suporta enviar push e pull por HTTP para seus repositórios Git remotos no Bitbucket. Toda vez que interagir com o repositório remoto, você deve fornecer uma combinação de nome de usuário/senha. Você pode armazenar essas credenciais, em vez de fornecer a combinação sempre, com o [Git Credential Manager para Windows](https://github.com/GitCredentialManager/git-credential-manager).

### Instale o Git com o Atlassian Sourcetree

O Sourcetree, um cliente visual gratuito do Git para Windows, vem com sua própria versão integrada do Git. Você pode [baixar o Sourcetree aqui](http://www.sourcetreeapp.com/br/).

Para aprender como usar o Git com o Sourcetree (e como hospedar seus repositórios Git no Bitbucket), você pode seguir o [Tutorial de Git com Bitbucket e Sourcetree](https://support.atlassian.com/bitbucket-cloud/docs/tutorial-learn-bitbucket-with-sourcetree/?_ga=2.64335407.1424849300.1543857612-1803500522.1531756517).

# Como criar um repositório

Para criar um novo repositório, você vai usar o comando `git init`.

git init` é um comando único que você usa durante a configuração inicial de um novo repositório. A execução desse comando cria um novo subdiretório `.git` no diretório de trabalho atual. Essa ação também vai criar uma ramificação principal.

## Clonando um repositório existente: git clone

Se um projeto já foi configurado em um repositório central, o comando clonar é a forma mais comum para os usuários obterem um clone de desenvolvimento local. Como o `git init`, a clonagem é geralmente uma operação única. Depois que um desenvolvedor obtiver uma cópia ativa, todas as operações de [controle de versão](https://bitbucket.org/product/br/version-control-software) serão gerenciadas pelo seu repositório local.

```bash
git clone <repo url>
```

`git clone` é usado para criar uma cópia ou clone de repositórios remotos. Você transmite o `git cline` em uma URL de repositório. O Git é compatível com alguns protocolos de rede diferentes e formatos correspondentes de URL. 



## Salvando alterações no repositório: git add e git commit

Agora que você possui um repositório clonado ou inicializado, é possível fazer commit em alterações de versão do arquivo nele. O exemplo seguinte pressupõe que você configurou um projeto em `/path/to/project`. Os passos a serem realizados neste exemplo são:

- Altere os diretórios para `/path/to/project`

- Criar um novo arquivo `CommitTest.txt` com o conteúdo ~"conteúdo de teste para o tutorial do Gitl"~

- Fazer git add `CommitTest.txt` na área de preparação de repositório

- Criar um novo commit com uma mensagem descrevendo o trabalho que foi feito no commit

  ```bash
  cd /path/to/project 
  echo "test content for git tutorial" >> CommitTest.txt 
  git add CommitTest.txt 
  git commit -m "added CommitTest.txt to the repo"
  ```

  Depois de executar este exemplo, seu repositório agora terá `CommitTest.txt` adicionado ao histórico e rastreará atualizações futuras do arquivo.

O Git armazena as opções de configuração em três arquivos separados, o que permite que você estenda as opções a repositórios individuais (local), usuário (Global) ou o sistema inteiro (sistema):

- Local: `/.git/config` – Configurações específicas dos repositórios.
- Global: `/.gitconfig` – Configurações específicas do usuário. É aqui que as opções definidas com o sinalizador --global são armazenadas.
- Sistema:``$(prefix)/etc/gitconfig – Configurações de todo o sistema.

Defina o nome do autor a ser usado para todas as confirmações no repositório atual. Em geral, o marcador usado para definir opções de configuração para o usuário atual é o `--global`.

```css
git config --global user.name <name>
```

Defina o nome do autor a ser usado para todas as confirmações pelo usuário atual.

Adicionar a opção `--local` ou não passar as opções de nível de configuração, definirá o `user.name` para o repositório local atual.

```bash
git config --local user.email <email>
```

## git add

O comando `git add` adiciona uma alteração no diretório ativo à área de staging. Ele diz ao Git que você quer incluir atualizações a um arquivo específico no próximo commit. No entanto, `git add` não tem efeito real e significativo no repositório — as alterações não são gravadas mesmo até você executar `git commit`.

Junto com esses comandos, você também vai precisar de `git status` para ver o estado do diretório ativo e da área de staging.

## Como funciona

Os comandos `git add` e `git commit` compõem o fluxo de trabalho fundamental do Git. Esses são os dois comandos que cada usuário do Git precisa entender, não importa o modelo de colaboração da equipe. Eles são os meios de gravar versões de um projeto no histórico do repositório.

O desenvolvimento de um projeto gira em torno do padrão básico editar/preparar/fazer commit. Primeiro, você edita os arquivos no diretório ativo. Quando estiver pronto para salvar uma cópia do estado atual do projeto, você prepara as alterações com `git add`. Depois que estiver satisfeito com a captura de tela montada, você faz commit no histórico do projeto com `git commit`. O comando `git reset` é usado para desfazer um commit ou captura de tela preparada.

Além de `git add` e `git commit`, um terceiro comando, `git push`, é essencial para um fluxo de trabalho colaborativo completo do Git. O `git push` é utilizado para enviar as alterações com commit para repositórios remotos para colaboração. Assim os outros membros da equipe podem acessar um conjunto de alterações salvas.

![Tutorial do Git: captura instantânea de git add](https://wac-cdn.atlassian.com/dam/jcr:0f27e004-f2f5-4890-921d-65fa77ba2774/01.svg?cdnVersion=836)

O comando `git add` não deve ser confundido com `svn add`, que adiciona um arquivo ao repositório. O `git add` funciona no nível mais abstrato de alterações. Ou seja: o `git add` precisa ser chamado toda vez que você altera um arquivo, enquanto o `svn add` precisa ser chamado apenas uma vez para cada arquivo. Pode parecer redundante, mas esse fluxo de trabalho faz com que seja muito mais fácil manter um projeto organizado.

## Opções comuns

```xml
git add <file>
```

Preparar todas as alterações em `<file>` para o próximo commit.

```xml
git add <directory>
```

Preparar todas as alterações em `<directory>` para o próximo commit.

```css
git add -p
```

Para criar um commit inicial do diretório atual, use os dois comandos a seguir:

```undefined
git add .
git commit
```