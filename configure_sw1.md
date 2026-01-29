`switch0> en`<br>
`switch0# conf t`<br>
`switch0(config)#hostname andr1`<br>
`andr1(config)# enable secret Tomil123` **задаём пароль на enable** <br>
`andr1(config)# service password-encryption ` <br>
`andr1(config)#vlan 2` <br>
`andr1(config-vlan)# name server` <br>
`andr1(config-vlan)# ex` <br>
`andr1(config)#vlan 3` <br>
`andr1(config-vlan)# name user` <br>
`andr1(config-vlan)# ex` <br>
`andr1(config)#vlan 4` <br>
`andr1(config-vlan)# name guest` <br>
`andr1(config-vlan)# ex` <br>
`andr1(config)#vlan 5` <br>
`andr1(config-vlan)# ip address 192.168.5.2 255.255.255.252 ` **Задаем ip на интерфейс коммутатора для удаленного подключения**<br>
`andr1(config-vlan)# ip default-gateway 192.168.5.1 ` **задаем шлюз по умолчанию** <br>
`andr1(config-vlan)# ex` <br>
`andr1(config)#int range f0/2-3 ` **переходим к настройке нескольких интерфейсов** <br>
`andr1(config-if-range)#switchport mode access ` **указываем что данный интерфейс является интерфейсом доступа**<br>
`andr1(config-if-range)#switchport access vlan 3  ` **указываем vlan этого интерфейса** <br>
`andr1(config)#int f0/1 `<br>
`andr1(config-if)#switchport mode access ` **указываем что данный интерфейс является интерфейсом доступа** <br>
`andr1(config-if)#switchport access vlan 2 ` **указываем vlan этого интерфейса**<br>
`andr1(config)#int f0/4 ` <br>
`andr1(config-if)#switchport mode access ` **указываем что данный интерфейс является интерфейсом доступа**<br>
`andr1(config-if)#switchport access vlan 4 ` **указываем vlan этого интерфейса** <br>
`andr1(config-if)#ex` <br>
`andr1(config)#int G0/1 ` <br>
`andr1(config-if)#switchport mode trunk ` **обозначаем интерфейс как trunk , это озночает что по нему теперь могут ходить тегированные frame** <br>
`andr1(config-if)#switchport trunk all vlan 2,3,4,5 `  <br>
`andr1(config-if)#ex` <br>
`andr1(config)# username admin privilege 15 secret Tomil123 ` **задаём пользователя с правами admina** <br>
`andr1(config)# username andrei privilege 0 secret Tomil123 ` **задаём пользователя с min правами**  <br>
`andr(config)# line console 0 ` **переходим в режим настройки консольного подключения** <br>
`andr(config-line)# login local ` **nребование аутентификации по локальной базе пользователей при подключении через консоль** <br>
`andr(config-line)#en` <br>
`andr(config)# line vty 0 15 ` **Переход в режим настройки виртуальных терминальных линий (VTY) с 0 по 15. Эти линии используются для удаленного доступа (Telnet/SSH).** <br>
`andr(config-line)# login local ` <br>
`andr(config-line)# transport input ssh ` **Разрешение только SSH подключений на VTY линиях** <br>
`andr(config-line)# en`<br>
`andr(config)#ip domain-name test1.local ` **Установка доменного имени для устройства. Это необходимо для генерации RSA ключей, которые используются в SSH**<br>
`andr(config)#crypto key generate rsa general-keys modulus 2048 ` **Генерируем ключи шифрования** <br>


