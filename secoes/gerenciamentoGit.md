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
