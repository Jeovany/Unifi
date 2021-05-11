# Atualizando firmware Unifi no modo online via SSH

1 - Acesse o site https://www.ui.com/download ;

--Selecione o modelo do seu rádio na coluna da esqueda;

--Após abrir o modelo selecionado, selecione a versão do firmware desejado e clique em File na última coluna do arquivo;

--Na janela de Download você poderá deverá clicar em copy url para copiar a url do arquivo a ser baixado;

2 - Conecte-se ao rádio utilizando seu seu terminal linux, digite o comando seguinte:

```shell
# ssh -v ip_host ou ssh -v ubnt@ip_hot (nesta sintaxe você informa o usuário de login)
```

--Na tela do rádio digite o seguinte comando e dê enter:

BusyBox v1.25.1 () built-in shell (ash)


  ___ ___      .__________.__
 |   |   |____ |__\_  ____/__|
 |   |   /    \|  ||  __) |  |   (c) 2010-2020
 |   |  |   |  \  ||  \   |  |   Ubiquiti Networks, Inc.
 |______|___|  /__||__/   |__|
            |_/                  https://www.ui.com/

      Welcome to UniFi UAP-AC-Lite!

BZ.v4.3.28# upgrade (cole aqui a url copiada do site da ubiquit)


* Exemplo:

BusyBox v1.25.1 () built-in shell (ash)


  ___ ___      .__________.__
 |   |   |____ |__\_  ____/__|
 |   |   /    \|  ||  __) |  |   (c) 2010-2020
 |   |  |   |  \  ||  \   |  |   Ubiquiti Networks, Inc.
 |______|___|  /__||__/   |__|
            |_/                  https://www.ui.com/

      Welcome to UniFi UAP-AC-Lite!

BZ.v4.3.28# upgrade https://dl.ui.com/unifi/firmware/(verãoDoFirmware).bin


***Aguarde o processo de atualização, neste momento você perderá a comunicação com o dispositivo, para monitorá-lo basta abrir um terminal ou prompt de comando de digitar ping ip_host.***

Após o processo finalizado basta realizar a adoção do dispositivo no controller ou caso já esteja adotado é só aguardar o dispositivo ficar on-line.



# Atualização de Unifi modo offline ou standAlone via SSH:

1 - Acesse o site https://www.ui.com/download ;

--Selecione o modelo do seu rádio na coluna da esqueda;

--Após abrir o modelo selecionado, selecione a versão do firmware desejado e clique em File na última coluna do arquivo;

--Na janela de Download você poderá optar em baixar o arquivo clicando em Download File;

2 - Para realizar a cópia do arquivo para o dispositivo primeiro devemos fazer algumas alterações:

--Em seu terminal acesse a pasta de download onde está seu arquivo;

--Temos renomear o arquivo para que não seja necessário a mudança dentro do dispositivo após a cópia.

```shell
# mv nome_arquivo fwupdate.bin
```

***Obs: Para qualquer versão de firmware o nome deverá sempre se o mesmo para upload.***

* Para copiarmos este arquivo para o rádio utilizaremos a ferramenta SCP - Secure Copy Protocol.

A sintaxe do comando é bem simples e segue essa regra:

scp scp [OPTION] [user@]SRC_HOST:]file1 [user@]DEST_HOST:]file2

Agora vamos realizar a cópia do arquivo para o rádio utilizando o seguinte comando:

```shell

# scp nome_arquivo usuario@ip_radio:caminho_pasta_destino
```

**Na documentação da Ubiquiti a pasta de destino deverá ser /tmp/**

```shell
# scp fwupdate.bin ubnt@ip_radio:/tmp/
```

**Após o colocar a senha do usuário uma barra de progressão será mostrada e informará o tempo restante até o final da transferência do arquivo.**

3 - Terminado o processo de cópia agora é hora de atualizar;

Conecte-se ao rádio via SSH utilizando seu seu terminal:

```shell
# ssh -v ubnt@ip_host
```

Certifique que na pasta /tmp/ o arquivo esteja lá digiando:

BusyBox v1.25.1 () built-in shell (ash)


  ___ ___      .__________.__
 |   |   |____ |__\_  ____/__|
 |   |   /    \|  ||  __) |  |   (c) 2010-2020
 |   |  |   |  \  ||  \   |  |   Ubiquiti Networks, Inc.
 |______|___|  /__||__/   |__|
            |_/                  https://www.ui.com/

      Welcome to UniFi UAP-AC-Lite!

BZ.v4.3.28# ls -l /tmp/

* A saída do comando deverá constar o arquivo:

```shell
BZ.v4.3.28:# ls -l /tmp/
-rw-r--r--    1 admin    root            31 May  9 03:06 TZ
-rw-r--r--    1 admin    root          3939 Dec 31  1969 default.cfg
drwxr-xr-x    2 admin    root            40 May  9 03:07 dropbear
lrwxrwxrwx    1 admin    root             4 Dec 31  1969 etc -> /etc
-rw-r--r--    1 admin    root       8028487 May 10 17:38 fwupdate.bin
-rw-------    1 admin    root             0 May  9 03:07 last-dump.core
drwxr-xr-x    3 admin    root            60 May  9 03:07 lib
drwxr-xr-x    2 admin    root            60 May  9 03:07 lock
drwxr-xr-x    2 admin    root           140 May 10 15:45 log
-rw-r--r--    1 admin    root           180 May 10 16:49 macs.guest.authorized
-rw-r--r--    1 admin    root         51241 May  9 03:08 rc.txt
lrwxrwxrwx    1 admin    root            21 May  9 03:06 resolv.conf -> /tmp/resolv.conf.auto
-rw-r--r--    1 admin    root            64 May  9 03:06 resolv.conf.auto
drwxr-xr-x    5 admin    root          1760 May 10 17:38 run
-rw-r--r--    1 admin    root         42139 May  9 03:06 running.cfg
drwxrwxrwt    2 admin    root            40 Dec 31  1969 shm
drwxr-xr-x    3 admin    root            60 May  9 03:07 spool
drwxr-xr-x    2 admin    root            40 Dec 31  1969 state
drwxr-xr-x    2 admin    root            80 Dec 31  1969 sysinfo
-rw-r--r--    1 admin    root         11620 May  9 03:06 sysinit.txt
-rw-r--r--    1 admin    root         42139 Dec 31  1969 system.cfg
drwxr-xr-x    2 admin    root            40 Dec 31  1969 tmp
drwxr-xr-x   10 admin    root           200 May  9 03:07 utermd
```

4 - Com o arquivo na pasta basta executar a atualização:

```shell
BZ.v4.3.24:# syswrapper.sh upgrade2 &
```

**Obs: Caso não lembre do nome do script syswrapper.sh, basta digitar sys e pressionar TAB que o será completado. Após a confirmação do comando e aguarde o processo de atualização, neste momento você perderá a comunicação com o dispositivo, para monitorá-lo basta abrir um terminal ou prompt de comando de digitar ping ip_host.**

Após o processo finalizado basta realizar a adoção do dispositivo no controller ou caso já esteja adotado é só aguardar o dispositivo ficar on-line.