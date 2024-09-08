# Lição 03

Nessa lição será abordado:
- Simulando comportamento de um dispositivo
- Chamadas do sistema de leitura e escrita

O objetivo da lição é demonstar as operações de ON e OFF, muitos comuns quando controlamos algum dispositivo físico. Para isso altere a função cusexmp_write do arquivo cuse.c com o seguinte código:
```
static void cusexmp_write(fuse_req_t req, const char *buf, size_t size,
			  off_t off, struct fuse_file_info *fi)
{
	(void)fi;

	const char cmd[4]="";
	uint8_t op=0;

	memcpy(&op, buf, 1);

	switch(op)
	{
		case 49:	
				memcpy(cmd,"ON\n",3);			
				break;
		case 50:
				memcpy(cmd,"OFF\n",4);	
				break;
		default:
				memcpy(cmd,"NOP\n",4);
				break;
	}

	if (cusexmp_expand(off + sizeof(cmd))) {
		fuse_reply_err(req, ENOMEM);
		return;
	}

	memcpy(cusexmp_buf + off, cmd, sizeof(cmd));

	fuse_reply_write(req, size);
}
```

Após realizar a alteração recompile para gerar um binário com essa mudança:
```
gcc -Wall cuse.c `pkg-config fuse3 --cflags --libs` -o cuse_licao_03
```
 Em seguida crie um dispositivo de caractere utilizando o parâmetro de debug:
```
sudo ./cuse_edited -f --name=meu_dispositivo -d
```

Agora para interagir com o dispositivo, precisamos enviar o comando que desejamos executar. Nesse exemplo ao enviar "1" o dispositivo deve ligar(ON), quando enviamos "2"(OFF) deve desligar e por último se mandarmos algum valor diferente dos mencionados o dispositivo não faz nada(NOP).

Para confirmar esse comportamento execute comando de ON:
```
echo "1" > /dev/meu_dispositivo
```

Verifique com:
```
cat /dev/meu_dispositivo
```

O resultado esperado é a exibição da string "ON" de forma contínua. Para finalizar pressione Ctrl+c.

Como exercício solicite ao público para testar outros valores quando utilizar o comando echo.

Outro ponto interessante dessa lição é demonstrar as chamadas do sistema de leitura e escrita. Quando executamos o echo redirecionando para o dispositido de caractere, é possível visualizar a chamada de sistema de escrita(WRITE) sendo chamada no terminal que foi criado o dispositivo. Enquanto realizado o comando cat, podemos visualizar a chamada READ sendo chamada sem parar.
Isso é um bom exemplo para demonstrar a interação entre a linha de comando e o driver de caractere.