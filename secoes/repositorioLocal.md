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
