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
