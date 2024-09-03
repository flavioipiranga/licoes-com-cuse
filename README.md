# licoes-com-cuse

## Instruções para compilar os exemplos de cuse contidos no FUSE-3.16.2
Obtendo o FUSE-3.16.2:
 wget https://github.com/libfuse/libfuse/releases/download/fuse-3.16.2/fuse-3.16.2.tar.gz

Extraia o arquivo baixado:

`tar xvf fuse-3.16.2.tar.gz`

Mude para o diretório contendo os exemplos:

`cd fuse-3.16.2/example`

Utilize o comando gcc para compilar o executável cuse:

`gcc -Wall cuse.c `pkg-config fuse3 --cflags --libs` -o cuse`

Verifique se o binário compilou corretamente:
 
 `./cuse --help`

O resultado esperado é de acordo com:
```
options:
    --help|-h             print this help message
    --maj=MAJ|-M MAJ      device major number
    --min=MIN|-m MIN      device minor number
    --name=NAME|-n NAME   device name (mandatory)
    -d   -o debug         enable debug output (implies -f)
    -f                    foreground operation`
    -s                    disable multi-threaded operation
```

Para compilar o exemplo cuse_client, utilize o comando:

`gcc -Wall cuse_client.c -o cuse_client`

Execure o binário gerado:

`./cuse_client`

O resultado esperado deve ser similar a:

```
Usage: cuse_client FIOC_FILE COMMAND

COMMANDS
  s [SIZE]     : get size if SIZE is omitted, set size otherwise
  r SIZE [OFF] : read SIZE bytes @ OFF (dfl 0) and output to stdout
  w SIZE [OFF] : write SIZE bytes @ OFF (dfl 0) from stdin
```
