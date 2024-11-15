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

### Visualizando *branches*

Executando apenas o comando ```branch``` é possível listar os nomes das *branches* existentes. 

```
git branch
```

### Excluindo uma *branch*

Para deletar *branches*, utiliza-se a *flag* ```-d``` ou ```--delete```. Normalmente, *branches* não são apagadas para que seja mantido um histórico de desenvolvimento.

```
git branch -d ramo_1
```
```
git branch --delete ramo_1
```
```
git branch -d ramo_1 ramo_2 ramo_3
```
```
git branch --delete ramo_1 ramo_2 ramo_3
```

### Trocando de *branch*

* Para sair da *branch* atual e selecionar outra já existente utilize o comando ``checkout``.

```
git checkout ramo_1
```

* Para criar uma *branch* e já selecioná-la utilize, também, a *flag* ``-b``.

```
git checkout -b ramo_1
```

### Renomeando uma *branch*

Para renomear uma *branch*, selecione-a e utilize o comando ``branch`` com a *flag* ``-M``. 

Anteriormente, o GitHub chamava a *branch* padrão de *master*. Agora, a nomenclatura oficial é *main*. Então, pode ser necessário renomeá-la.

```
git branch -M main
```

### Juntando *branches*

Utilize o comando ``merge`` para juntar a *branch* especificada com a selecionada.

```
git merge main
```

### Comparando *branches*

Diferenças entre duas *branches* podem ser visualizadas com o já conhecido comando ``diff``.

```
git diff ramo_1 ramo_2
```

### Verificando o histórico

É possível visualizar o histórico de *commits* de uma *branch* através do comando ``log``. *Flags* podem ser utilizadas para filtrar a lista exibida, a seguir serão apresentadas algumas delas.

```
git log
```

* Exibição dos **n** *commits* mais recentes

A *flag* ``-n`` define a quantidade específica de *commits* a ser retornada

```
git log -n 4 //retorna os 4 últimos commits
```

* Exibição dos *commits* escritos por alguém específico

Para filtrar a lista exibida por quem escreveu, use o *parâmetro* ``--author``.

```
git log --author=fulano //retorna os commits feitos por "fulano"
```

* Exibição dos *commits* que afetam um arquivo específico

Utilize ``--`` para especificar os arquivos que sofreram alterações em *commits*.

```
git log -- tutorial.txt
```
```
git log -- tutorial.txt index.html estilo.css
```

* Exibindo apenas o assunto da mensagem dos *commits* 

O parâmetro ``--oneline`` especifica que o histórico exibirá apenas o ID do *commit* junto com a primeira linha da mensagem associada a ele.

```
git log --oneline
```

* Exibição resumida dos *commits*

Para exibir um ``log`` de forma resumida, use o comando ``shortlog`` ao invés de ``log``. A lista de *commits* já feitos será agrupada por autor, exibindo o assunto da mensagem dos *commits* em ordem cronológica começando pelo mais antigo.

```
git shortlog
```

* Exibindo os *commits* de todas as *branches*

O parâmetro ``--all`` permite visualizar o histórico de *commits* de todas as *branches*. Utilize, também, ``--graph`` para uma melhor leitura.

```
git log --all --graph
```

### Desfazendo alterações

Existem comandos que possibilitam uma *branch* voltar a um estado de acordo com um *commit* especificado.
 
A especificação do *commit* é feita através do seu ID. Para *commits* recentes também pode-se usar a referência HEAD ou HEAD\~n (Por exemplo, HEAD\~1 é o penúltimo *commit* e HEAD\~2 é o antepenúltimo).

#### **Desfazendo _commits_ mantendo o histórico**

Com o comando ``revert``, as alterações posteriores ao *commit* especificado são invertidas, e gera-se um novo *commit* representando o estado anterior ao especificado. Deste modo, o histórico permanece intacto, nada é apagado. Seu uso é recomendado quando deseja-se desfazer alterações que já estão no repositório remoto, para não afetar outras tarefas em desenvolvimento. 

Utilizando o parâmetro ``--no-edit`` pula-se a edição da mensagem do *commit* e a padrão é adicionada.

```
git revert HEAD
```
```
git revert HEAD --no-edit
```
```
git revert 9a9add8
```

#### **Desfazendo _commits_ alterando o histórico**

O comando ``git reset`` traz a *branch* para um estado anterior sem fazer um novo *commit*. Todo *commit* posterior ao *commit* especificado é descartado.

É preciso cautela com o uso deste comando pois ele modifica o histórico da *branch*. Seu uso é recomendado para desfazer *commits* que estão apenas no repositório local. 

Apesar dos *commits* desaparecerem do histórico, eles não são removidos do Git. Quando se conhece o ID de algum já apagado é possível aplicar o ``reset`` nele. Tais *commits* que não estão no histórico são excluidos permanentemente após a execução do coletor de lixo interno do Git, que é executado por padrão a cada 30 dias.

Existem três *flags* que definem como o comando será executado: ``--soft``, ``--mixed`` e ``--hard``. Omitindo-se o parâmetro e a referência do *commit* são definidos implicitamente ``--mixed`` e HEAD, respectivamente.

* O parâmetro ``--soft`` mantém as alterações do diretório de trabalho e as pendências da área de *staging*. Deste modo, apenas o histórico de *commits* é redefinido. 

```
git reset --soft 9a9add8
```
```
git reset --soft HEAD
```
```
git reset --soft //igual ao comando acima
```

* O parâmetro ``--mixed`` corresponde a execução padrão do comando ``reset``. As pendências da área de *staging* são transferidas para o diretório de trabalho como alterações.

```
git reset --mixed 9a9add8
```
```
git reset 9a9add8 //igual ao comando acima
```
```
git reset --mixed HEAD
```
```
git reset //igual ao comando acima
```

* Com o parâmetro ``--hard``, as alterações do diretório de trabalho e as pendências da área de *staging* são apagadas.

```
git reset --hard 9a9add8
```
```
git reset --hard HEAD
```
```
git reset --hard  //igual ao comando acima
```
