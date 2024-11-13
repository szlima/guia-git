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
