## Laboratory work XI

Данная лабораторная работа посвещена изучению процесса создания сеансов совместной разработки с использованием инструмента **ngrok**

```sh
$ open https://ngrok.com/
```

## Tasks

- [+] 1. Ознакомиться со ссылками учебного материала
- [+] 2. Выполнить инструкцию учебного материала
- [+] 3. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ cd ~
$ mkdir install
$ mkdir tmp
$ export HOME_PREFIX=`pwd`/install
$ echo $HOME_PREFIX
$ export USERNAME=`whoami`
```

```sh
$ cd tmp
```

```sh
$ wget https://github.com/libevent/libevent/releases/download/release-2.1.8-stable/libevent-2.1.8-stable.tar.gz - качаем libevent-2.1.8
$ tar -xvzf libevent-2.1.8-stable.tar.gz - разархивируем
$ cd libevent-2.1.8-stable
$ ./configure --prefix=${HOME_PREFIX} - устанавливаем компоненты программы
$ make && make install - сборка и компиляция
$ cd ..
```

```sh
$ wget http://invisible-island.net/datafiles/release/ncurses.tar.gz - скачиваем библиотеку ncurses
$ tar -xvzf ncurses.tar.gz - разархивируем
$ cd ncurses-5.9
$ ./configure --prefix=${HOME_PREFIX} - устанавливаем компоненты программы
$ make && make install - сборка и компиляция
$ cd ..
```


```sh
$ wget https://github.com/tmux/tmux/releases/download/2.5/tmux-2.5.tar.gz - скачиваем tmux
$ tar -xvzf tmux-2.5.tar.gz
$ cd tmux-2.5
$ ./configure --prefix=${HOME_PREFIX} CFLAGS="-I${HOME_PREFIX}/include -I${HOME_PREFIX}/include/ncurses" LDFLAGS="-L${HOME_PREFIX}/lib"
$ make && make install
$ cd ..
```

```sh
$ wget https://bin.equinox.io/c/4VmDzA7iaHb/ngrok-stable-linux-amd64.zip - скачиваем ngrok
$ unizp ngrok-stable-linux-amd64.zip
$ mv ngrok ${HOME_PREFIX}/bin
```

```sh
$ export LD_LIBRARY_PATH=${HOME_PREFIX}/lib
$ export PATH="${HOME_PREFIX}/bin:${PATH}"
$ tmux - открываем терминал
```

```sh
$ cd ~
$ rm -rf tmp install
```

```sh
$ brew install tmux ngrok # or use linuxbrew 🎉  -устанаваливаем tmux и ngrok
```

```sh
$ tmux new -s session_with_group
```

```sh
# Alisa:
$ open https://ngrok.com/signup авторизируемся и берем токен
$ export NGROK_TOKEN=<токен>
$ ngrok authtoken ${NGROK_TOKEN} - авторизируемся
$ ngrok tcp 22 - создаем тунел с портом 22
<порт_ngrok_сервера>
```

```sh
# Bob:
$ ssh ${USERNAME}@0.tcp.ngrok.io -p<порт_ngrok_сервера> - через протокол ssh установить соединение с открытой сессий в нгрок
<пароль_от_учетной_записи>
<пароль_от_учетной_записи>
$ tmux a -t session_with_group -присоединиться к сессии
$ <C-B>" - разделяем экран
```

## Report

```sh
$ cd ~/workspace/
$ export LAB_NUMBER=11
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Links

- [Tmux](https://raw.githubusercontent.com/tmux/tmux/master/README)
- [Libevent](http://libevent.org)
- [Ncurses](http://invisible-island.net/ncurses/)

```
Copyright (c) 2015-2021 The ISC Authors
```
