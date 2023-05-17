# Guia de Git/GitHub

## Comandos básicos

### Área de *staging*

O espaço de preparação para um *commit* é chamado **_staging_**. Quando um *commit* é efetuado, todos os itens da área de *staging* são inseridos nele. Assim, arquivos que estão no *staging* estão prontos para serem *commitados*.

#### **Adicionando arquivos**

O comando ``add`` transfere arquivos novos ou monitorados com alterações para a área de *staging*. É possível adicionar um único arquivo, vários ou até mesmo todos de uma só vez.

```
git add tutorial.txt
```
```
git add tutorial.txt index.html estilo.css
```
```
git add . //adiciona todos os arquivos
```
```
git add --all //igual ao comando acima
```
```
git add -A //igual ao comando acima
```

#### **Removendo arquivos**

A remoção de arquivos da área de *staging* é feita com o comando ``rm`` junto com o parâmetro ``--cached``. Utilize, também, a *flag* ``-r`` junto com o seletor ``.`` caso seja necessário remover tudo do *staging*.

```
git rm --cached tutorial.txt
```
```
git rm --cached tutorial.txt index.html estilo.css
```
```
git rm --cached -r .  //remove todos os arquivos
```

#### **Desfazendo modificações**

Para desfazer as últimas mudanças de arquivos monitorados e fazê-los voltar ao seu último estado de atualização, utilize o comando ```checkout```. 

```
git checkout tutorial.txt
```
```
git checkout tutorial.txt index.html estilo.css
```
```
git checkout . 
```

### Commitando

Um *commit* marca uma etapa alcançada durante o processo de desenvolvimento. Pode-se dizer que ele salva um grupo de alterações significativas.

No decorrer de um projeto os arquivos vão sendo alterados. Arquivos monitorados modificados passam a estar atualizados após um *commit*. Cada uma de suas versões consegue ser encontrada através do histórico de *commits*. 

Todo *commit* possui um identificador, um autor e o momento em que foi realizado. Seu hash de identificação é exclusivo, um código SHA-1, e este ID também possui uma versão reduzida com 7 caracteres.

#### **Realizando _commits_**

Utiliza-se o comando ``commit`` para realizar esta ação, ele é representado por uma mensagem através da *flag* ``-m``.

```
git commit -m "Mensagem que descreve o commit"
```

Também pode-se incluir a *flag* ``-a``. Esta ação inclui automaticamente todos os arquivos monitorados modificados, mesmo aqueles que não estavam na área de *staging*.

```
git commit -a -m "Mensagem que descreve o commit"
```

## Manipulando arquivos

### Ignorando arquivos

Ao criar na raíz do repositório um arquivo chamado **.gitignore**, especifica-se o que deve ser ignorado pelo Git. Arquivos específicos, com uma determinada extensão ou até mesmo o próprio arquivo .gitignore não serão incluídos nas atualizações do projeto. 

O exemplo abaixo mostra a escrita de um caso em que seriam ignorados o arquivo tutorial.txt, tudo o que possui a extensão .log, a pasta senhas e o próprio .gitignore.

```
tutorial.txt
*.log
senhas/
.gitignore
```

### Renomeando arquivos

Para renomear um arquivo, ou mover ele para outra pasta, utilize o comando ``mv``.

```
git mv antes.txt depois.txt
```
```
git mv tutorial.txt textos/tutorial.txt
```

### Excluindo arquivos

O já conhecido comando ``rm`` também remove definitivamente arquivos monitorados do projeto. Para executar a operação para todos utilize a *flag* ``-r`` junto com o seletor de todos os arquivos ``.``.

* Para arquivos não modificados utilize apenas ``rm``. 

```
git rm tutorial.txt
```
```
git rm tutorial.txt index.html estilo.css
```
```
git rm -r . //remove todos os arquivos
```

* Para arquivos modificados utilize, também, a *flag* ``-f``.

```
git rm -f tutorial.txt
```
```
git rm -f tutorial.txt index.html estilo.css
```
```
git rm -f -r . //remove todos os arquivos
```

### Analisando mudanças em arquivos

Todas as alterações em arquivos monitorados podem ser visualizadas através do comando ``diff``. De acordo com os casos abaixo, quando utilizado o comando com o nome de um ou mais arquivos serão exibidas apenas as diferenças referentes a este(s) arquivo(s). As modificações são apresentadas de modo que uma versão é assinalada pelo caractere '-' e outra pelo caractere '+'.

* Executando o comando sem *flags*, são apresentadas as diferenças entre o diretório de trabalho e a área de *staging*. Ou seja, mostra-se as alterações dos arquivos que não foram incluídas no *staging*.

```
git diff 
```
```
git diff tutorial.txt 
```
```
git diff tutorial.txt index.html 
```

* Utilizando o comando ``diff`` com o parâmetro ``--cached`` ou ``--staged``, são apresentadas as diferenças entre o que já está no *staging* e o *HEAD*.

```
git diff --cached
```
```
git diff --staged
```
```
git diff --staged tutorial.txt 
```
```
git diff --staged tutorial.txt index.html 
```

* Aplicando o comando ``diff`` no *HEAD*, são apresentadas todas mudanças dos arquivos com relação ao último *commit*.

```
git diff HEAD
```
```
git diff HEAD tutorial.txt 
```
```
git diff HEAD tutorial.txt index.html 
```

## O que é *branch*?

Repositórios Git iniciam com uma linha padrão de desenvolvimento. A partir desta linha podem ser desenvolvidas ramificações. Todas as linhas existentes em um projeto são denominadas *branches*.

A *branch* padrão é denominada como base/mestra/principal. O GitHub a nomeia como *main* em repositórios novos. 

Novas *branches* podem ser criadas para isolar o desenvolvimento de diferentes funcionalidades sem afetar o código já testado e estável. Assim, em uma parte separada, é possível desenvolver recursos (*features*) ou corrigir erros com segurança.

### Criando uma *branch*

Uma *branch* nova é criada a partir de uma *branch* já existente, normalmente esta *branch* de referência é a padrão. A nova ramificação inicia como uma cópia da outra e pode ser modificada de forma independente de todo o resto do projeto. 

O comando a seguir cria uma *branch* a partir da que está selecionada no momento. 

```
git branch ramo_1
```
