# :octocat: Guia de Git/GitHub

Em 2005, Linus Torvalds criou um sistema de controle de versão chamado **Git**. Este mecanismo salva as alterações de um projeto ao longo do tempo sem sobrescrever as versões anteriores. Assim, o controle de versão possibilita o acompanhamento de mudanças, além da colaboração na codificação. Outros sistemas de controle de versão também conhecidos são o SVN e o CVS.

O Git estabelece um repositório como uma estrutura para armazenar metadados de um conjunto de arquivos e pastas. São registrados o grupo de arquivos e o histórico de suas alterações. Cada projeto possui seu respectivo repositório, onde este é considerado a pasta que contém todos os dados relacionados a ele.

O **GitHub** é uma plataforma que hospeda códigos-fonte e arquivos utilizando o Git em seu gerenciamento. Ele funciona como um repositório à distância (remoto) para projetos locais. Além do GitHub existem outros serviços de hospedagem semelhantes, como o GitLab e o BitBucket.

## Começando um repositório local

### Começando do zero

O comando a seguir inicializa um repositório Git vazio no respectivo diretório. Esta ação gera uma pasta invisível ``.git`` que permitirá o uso do sistema de versionamento.

```
git init
```

### Partindo de um projeto já existente

Com o comando ``clone``, um repositório já inicializado será clonado no respectivo diretório, assim a pasta invisível ``.git`` já terá sido criada. O local de onde vem o clone pode ser a URL de um repositório remoto ou o caminho de um diretório local.

```
git clone https://github.com/fulano/repo-git .
```
```
git clone /home/fulano/pastaprojetooriginal .
```

## O gerenciamento do Git

O Git gerencia e manipula o conteúdo do repositório local em três áreas diferentes, também conhecidas como três árvores: diretório de trabalho (*working directory*), área de *staging* (*index*) e histórico de *commits* (*HEAD*). Estas áreas são estruturas utilizadas para monitorar a linha do tempo das edições da *branch* selecionada. O Git registra os estados do projeto, manipulando as três árvores.

Um repositório Git é como uma árvore de *commits*, onde cada um aponta para o seu antecessor. Ao efetuar um *commit*, atualiza-se o *HEAD* para apontar para o *commit* mais recente. 

* **Diretório de trabalho:** área onde os arquivos do projeto estão localizados e disponíveis para edições antes de seu envio para a área de *staging*.

* **Área de _staging_:** local das alterações propostas para o próximo *commit*, representa uma área de preparação para um novo estado do histórico.

* **_HEAD_:** ponteiro para a referência da *branch* selecionada, tal como é um ponteiro para o último *commit* feito naquela *branch*. Portanto, *HEAD* representa o estado definido pelo último *commit* do histórico.

### Verificando o estado das três áreas

O comando ``git status`` apresenta a situação dos arquivos com relação a estas áreas. Quando não existem mudanças significa que as três áreas estão iguais. Assim, toda vez que a *branch* está atualizada quer dizer que os arquivos no diretório de trabalho e na área de *staging* estão iguais ao estado do *HEAD*.

Este comando exibe os arquivos novos e os monitorados com modificações. São descritos aqueles que já estão incluídos no *staging* e os que não estão.

```
git status
```

A seguir são apresentados os estados de arquivos no Git.

* Não monitorado (*untracked*): Arquivo novo que ainda não foi adicionado ao gerenciamento do Git.

* Adicionado (*added*): Arquivo novo que foi incluído na área de *staging*. Após o *commit* passará a ser monitorado.

* Modificado (*modified*): Arquivo monitorado que sofreu alterações.

* Preparado (*staged*): Arquivo monitorado que sofreu alterações e foi adicionado a área de *staging*.

* Atualizado (*comitted*): Arquivo que foi incluído num *commit* e está atualizado de acordo com o *HEAD*.

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

## Utilizando repositórios remotos

Um repositório remoto corresponde a uma versão do projeto local que está hospedada em uma rede. Desta forma, um trabalho pode ser compartilhado entre um time via Internet, por exemplo. Cada membro pode ter uma cópia local e independente, esta pode ser alterada e ter suas mudanças enviadas para a versão remota.

A comunicação entre os repositórios local e remoto é feita através de uma conexão que é definida localmente. Esta conexão é nomeada e cria-se na máquina local um repositório que é como um espelho do remoto.

*Origin* é um nome padrão para uma conexão remota. Porém, caso exista mais de um remoto vinculado ao repositório local é importante nomeá-los de forma autoexplicativa.

Quando um projeto é carregado via ``git clone``, cria-se automaticamente um remoto chamado *origin*, cuja conexão direciona para o repositório clonado.

* **Os conceitos _upstream_ e _downstream_**

Os termos *upstream* e *downstream* dizem respeito a repositórios. O gerenciamento do Git trabalha com o conceito de fluxo de registros de momentos específicos (*stream of snapshots*).

*Upstream* equivale ao projeto de origem, à fonte. *Downstream* corresponde a um projeto que deriva do original. Este projeto derivado pode ser gerado através de um *fork* ou um *clone*, por exemplo. Desta forma, uma referência *upstream* dele poderia ser o remoto *origin*.

Uma ação *upstream* representa um fluxo que vai no sentido da fonte. Assim como no conceito de *upload* seria algo que é inserido, como um *push*, por exemplo. Já uma ação *downstream* seria um fluxo que vem no sentido da fonte para o repositório derivado. Assim como no conceito de *download* seria algo que é baixado, como um *pull*, por exemplo.

### Configurando remotos

#### **Adicionando um repositório remoto**

 Utilize o comando ``remote`` junto com ``add`` para criar uma conexão entre o repositório local e um repositório remoto. O exemplo a seguir adiciona uma conexão para a URL informada e nomeia-a como *origin*.

```
git remote add origin https://github.com/fulano/repo-git.git
```

#### **Removendo um repositório remoto**

Para excluir a conexão com um repositório remoto utilize o comando ``remote`` com ``remove``, além do nome do remoto.

```
git remote remove origin
```

#### **Visualizando os repositórios remotos**

Para listar todos os repositórios remotos salvos utilize apenas o comando ``remote``.

```
git remote
```

#### **Visualizando o endereço de um repositório remoto**

Para visualizar a URL de um repositório remoto utilize o comando ``remote`` com ``get-url``, especificando o nome do remoto.

```
git remote get-url origin
```

#### **Trocando o endereço de um repositório remoto**

Para alterar a URL de um repositório remoto utilize o comando ``remote`` com ``set-url``, especificando o nome do remoto e o novo endereço.

```
git remote set-url origin https://github.com/fulano/repo-git.git
```

### Interagindo com remotos

#### **Enviando alterações**

* Para enviar *branch(es)* atualizada(s) para o repositório remoto, especifique seu(s) nome(s) e utilize o comando ``push``. Os exemplos a seguir mostram envios para o repositório remoto *origin*.

```
git push origin main
```
```
git push origin ramo_1 main
```

* Para já deixar configurada a conexão remota de *branches* locais, utilize a *flag* ``-u`` ou ``--set-upstream``. Nos *pushes* seguintes será possível enviar a *branch* selecionada sem especificar seu nome nem seu remoto correspondente.

```
git push -u origin main
```
```
git push --set-upstream origin main
```
```
git push -u origin main ramo_1
```
```
git push --set-upstream origin main ramo_1
```
```
git push //execução do push p/ branch selecionada após algum dos usos acima
```

* Para enviar todas as *branches* atualizadas para o remoto, utilize o parâmetro ``--all``.

```
git push --all
```

#### **Recebendo alterações**

O comando ``fetch`` baixa atualizações do repositório remoto, mas sem aplicá-las ao local. O repositório espelho do remoto que está na máquina local é atualizado em relação às suas referências remotas. Assim, é possível verificar o que há de novo antes de integrar à cópia em desenvolvimento.

##### **Baixando alterações**

* Para baixar atualizações de *branches* específicas, utilize ``fetch`` junto com o nome do remoto e o nome da(s) *branch(es)*.

```
git fetch origin ramo_1
```
```
git fetch origin ramo_1 main
```

* Para baixar todas as atualizações de um repositório remoto, utilize ``fetch`` junto com o nome do remoto.

```
git fetch origin
```

Quando o nome do repositório não é especificado é feito um ``fetch`` do remoto configurado para a *branch* selecionada. Caso esta *branch* não esteja configurada o ``fetch`` vem do repositório padrão (normalmente é o *origin*).

```
git fetch 
```

* Para baixar todas as atualizações de todos os remotos registrados, utilize ``fetch`` junto com o parâmetro ``--all``.

```
git fetch --all
```

##### **Verificando e aplicando alterações**

Após baixar as atualizações é possível verificar as mudanças acessando as *branches* remotas. Com o já conhecido comando ``branch`` liste todas as *branches* existentes. Utilize a flag ``-r`` para ver apenas as *branches* remotas ou ``-a`` para ver todas as *branches*, locais e remotas.

```
git branch -r
```
```
git branch -a
```

Após ver a lista de *branches* disponíveis, verifique as atualizações de uma *branch* remota com o comando ``checkout``, basta especificar o remoto junto ao seu nome. 

Por exemplo, considerando uma *branch* local main, sua versão num repositório remoto chamado *origin* seria origin/main. A seguir é apresentado como seria a seleção desta *branch* remota.

```
git checkout origin/main
```

Para comparar as diferenças pode-se executar o comando ``diff``.
```
git diff main origin/main
```

Para aplicar as atualizações localmente basta selecionar a *branch* local e executar um ``merge`` com a versão remota. No exemplo a seguir, estando a *branch* main selecionada, ocorre a sua mesclagem com a versão remota.

```
git merge origin/main
```

Pode-se criar uma *branch* a partir de uma remota caso ela não exista localmente. Nos exemplos a seguir, estando a *branch* remota selecionada, cria-se uma *branch* chamada ramo_1.

```
git branch ramo_1 // cria uma nova branch local a partir da remota selecionada
```
```
git checkout -b ramo_1 //cria e seleciona a nova branch local
```

#### **Recebendo e aplicando alterações**

Anteriormente foi apresentado como receber atualizações remotas e aplica-las localmente. Existe, porém, um comando que já executa as duas ações de uma vez. 

O comando ``pull`` é uma *shorthand* que corresponde a execução dos comandos ``fetch`` e ``merge``. Assim, ele baixa as atualizações remotas e aplica na *branch* local selecionada as modificações da sua referência remota.

* Para baixar todas as atualizações de um repositório remoto e aplicar na *branch* selecionada o que está disponível na sua referência remota, utilize ``pull`` junto com o nome do remoto.

```
git pull origin
```

Considerando que a *branch* selecionada é a main e a sua referência remota é origin/main, o comando acima é equivalente aos comandos a seguir. Caso o remoto da *branch* selecionada fosse outro não seriam aplicadas atualizações.

```
git fetch origin
git merge origin/main
``` 

Quando o nome do repositório não é especificado é feito um ``pull`` do remoto configurado para a *branch* selecionada. Caso esta *branch* não esteja configurada o ``pull`` vem do repositório padrão (normalmente é o *origin*).

```
git pull 
```

Para configurar um remoto para uma *branch* execute o comando a seguir. Consideramos, para exemplificar, a *branch* local como main, e o seu remoto como origin/main.

```
git branch --set-upstream-to=origin/main main
```

* Para baixar apenas as atualizações de uma *branch* específica e aplica-las na branch selecionada utilize o comando ``pull`` junto com o nome do remoto e o nome da *branch* específica.

```
git pull origin main
```

Considerando que a *branch* selecionada é a main e a sua referência remota é origin/main, o comando acima é equivalente aos comandos a seguir. É preciso atenção para qual *branch* está selecionada pois será realizado um merge dela com a versão remota especificada.

```
git fetch origin main
git merge origin/main
```

* Para baixar todas as atualizações de todos os repositórios remotos registrados e aplicar na *branch* selecionada o que está disponível na sua referência remota, utilize ``pull`` junto com o parâmetro ``--all``.

```
git pull --all
```

Considerando que a *branch* selecionada é a main e a sua referência remota é origin/main, o comando acima é equivalente aos comandos a seguir.

```
git fetch --all
git merge origin/main
```

### Procedimentos no GitHub

#### **Solicitando aprovações**

Uma solicitação de *pull*, ou um _**pull request**_ (PR), é um procedimento em que um membro da equipe notifica aos outros a conclusão de uma funcionalidade.

Após enviar todo o seu conteúdo local para sua conta no GitHub, este membro solicita através dela a inclusão do que foi desenvolvido no código oficial. Assim, a *branch* que contém a funcionalidade terá seu conteúdo analisado. Caso sejam necessárias alterações há um ambiente para trocas de mensagens, onde as melhorias podem ser debatidas. Então, quando o(s) membro(s) responsável(is) finalizam a revisão e aprovam a funcionalidade, um *merge* desta *branch* com a principal é executado.

O *pull request* possibilita um controle do que é incluido na *branch* principal do projeto, deste modo garante-se que lá haverão apenas tarefas concluídas. A seguir são apresentadas algumas nomenclaturas relacionadas a este procedimento.

* *Reviewers*: Membros da equipe que receberão a solicitação de *pull*, revisarão o código e aprovarão o *merge* com a *branch* principal.

* *Assignees*: Membros da equipe responsáveis pelo *pull request*. Exemplo: pode ser a pessoa que abriu o *pull request*.

* *Labels*: Etiquetas sobre o assunto do *pull request*. Exemplos: *bug* e *enhancement*.

Após uma solicitação de *pull request*, pode-se fazer outros *commits* na *branch*. Estes ainda serão integrados no PR já feito.

#### **Clonando projetos**

O GitHub possibilita a clonagem de um repositório qualquer para sua própria conta através de um procedimento chamado *fork*. 

Ao selecionar a opção *fork* no repositório desejado, ele é inteiramente copiado com todo o seu histórico. Desta forma, é possível realizar modificações separadamente em sua conta, sem afetar o projeto original.

Com o *fork*, é possível contribuir em projetos de terceiros com menos riscos de alterações indevidas. Geralmente são executados os seguintes passos: 

1. *Fork* do projeto para a conta pessoal
2. Clonagem deste novo projeto para sua máquina local
3. Execução das mudanças necessárias
4. Envio das alterações para o repositório da sua conta no GitHub
5. Realização de um *pull request* para que as mudanças sejam integradas no projeto original

## Referências

* https://git-scm.com/book/pt-br/v2
* https://petcomputacaoufrgs.github.io/intro-ao-git/
* https://www.w3schools.com/git/
* http://www-cs-students.stanford.edu/~blynn/gitmagic/intl/pt_br/
* https://www.atlassian.com/br/git/tutorials
* https://github.com/git-guides
* https://docs.github.com/pt/pull-requests
* https://www.javatpoint.com/git
* https://www.freecodecamp.org/news/how-to-fork-a-github-repository/

:star: Este guia lhe ajudou? Por favor, **deixe a sua estrela** aqui! :star:

:question: Algo parece confuso ou você tem dúvidas? Vamos conversar: [E-mail](mailto:suzanelima@outlook.com)