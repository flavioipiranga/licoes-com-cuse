# Lição 02

Nessa lição será abordado:
- Funcionamento da operação de escrita

Crie um dispositivo de caractere utilizando o comando:
```
sudo ./cuse -f --name=meu_dispositivo &
```

Envie uma string(cadeia de caractere) para o dispositivo com o comando:
```
echo "ola" | sudo ./cuse_client /dev/meu_dispositivo w 4
```

Execute a leitura dos dados presentes no dispositivo:
```
sudo ./cuse_client /dev/meu_dispositivo r 4
```

Mostre ao público que a palavra está sendo exibida corretamente conforme esperado.

Agora execute a operação de escrita com tamanho 1:
```
echo "ola" | sudo ./cuse_client /dev/meu_dispositivo w 1
```

E na sequência com tamanho 2:

```
echo "ola" | sudo ./cuse_client /dev/meu_dispositivo w 2
```

Mais uma vez, mencione que não ocorreu nenhuma alteração na palavra exibida. Agora execure usando tamanho 1 e mudando a palabra para "mundo":
```
echo "mundo" | sudo ./cuse_client /dev/meu_dispositivo w 1
```

Pergunte agora o que mudou uma vez que a palavra exibida se tornou mla. Após a interação é possível explicar que a operação de escrita escreve de forma contínua, logo quando utilizamos ola, nada mudou pois estava sendo feita a reescrita da mesma palavra. Quando alteramos para "mundo", a primeira letra de "mundo" foi reescrita na primeira letra de "ola", resultando em "mla"

Por fim, como exercício peça ao público que execute a seguinte escrita:
```
echo "mundo" | sudo ./cuse_client /dev/meu_dispositivo w 6
```

Na sequência outra escrita:
```
echo "ola" | sudo ./cuse_client /dev/meu_dispositivo w 5
```

Por fim uma leitura:
```
sudo ./cuse_client /dev/meu_dispositivo r 6
```

O exercício é explicar o resultado final:
```
ola
o
```

A resposta é que a segunda escrita foi realizada com 4 bytes, apesar do uso do tamanho 5 e dessa forma as letras "mund" foram substituídas por "ola" e o caractere de nova linha, jogando assim a útlima letra "o" restante para baixo.