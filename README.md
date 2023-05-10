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
