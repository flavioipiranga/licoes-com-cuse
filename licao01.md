# Lição 01 

Nessa lição será abordado:
- Criação de um dispositivo de caractere
- Uso das funções leitura e escrita
- Explicação do funcionamento do comando echo

Crie um dispositivo de caractere utilizando o comando:
```
sudo ./cuse -f --name=meu_dispositivo &
```

Envie uma string(cadeia de caractere) para o dispositivo com o comando:
```
echo "hello" | sudo ./cuse_client /dev/meu_dispositivo w 6
```

Ao utilizar o comando de escrita, pode ser um bom momento para interagir com o público perguntando o motivo de o número utilziado ser 6 ao invés de apenas 5, pois a palavra "hello" tem apenas 5 caracteres.

Depois execute a leitura dos dados presentes no dispositivo:
```
sudo ./cuse_client /dev/meu_dispositivo r 6
```

Ao utilizar o comando de leitura, pode ser interessante executar novamente com o número 5 para perguntar ao público qual a diferença entre eles.

Por fim, o indivíduo responsável pela lição explica a respeito do funcionamento do comando echo. Abordando que esse comando introduz por padrão o caractere "\n" representando uma nova linha. Explicando assim o motivo de precisarmos ter o número de caracteres da palavra adicionado de mais um para representar o caractere de nova linha.
