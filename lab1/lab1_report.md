University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Network programming](https://github.com/itmo-ict-faculty/network-programming)

Year: 2024

Group: K34202

Author: Islamov Sergey Sergeevich

Lab: Lab1

Date of create: 26.09.2024

Date of finished: 26.09.2024

Тема работы: Установка CHR и Ansible, настройка VPN

Цель работы: развертывание виртуальной машины с установленной системой контроля конфигураций Ansible и установка CHR в VirtualBox

Ход работы:
1. Создаём виртуальную машину в GCP на операционной системе Ubuntu 20.04.

2. Подключаемся к ней по ssh, устанавливаем ansible.

![image](https://github.com/16Angeles/2024_2025-network_programming-k34202-islamov_s_s/blob/ea4d2f1594cdc28d2dcd805289e1f40303b1c026/lab1/ans.jfif)

4. В VirtualBox устанавливаем MikroTik, это будет важно для дальнейшей работы. Здесь имеет смысл обратить внимание на то, что после загрузки в настройках VirtualBox необходимо отключить загрузочный диск вручную, тогда как на установке более привычных операционных систем это происходит автоматически.

5. После этого устанавливаем Wireguard на удалённую машину, прописываем в нём в файл условий интерфейса. Создаём пару ключей.

![image](https://github.com/16Angeles/2024_2025-network_programming-k34202-islamov_s_s/blob/e501baf5996ae1b39417675e0ed3d0fe913231be/lab1/%D0%BA%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%20%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80%D0%B0.jfif)

6. После этого начинаем работу с MikroTik. С помощью WinBox открываем графический интерфейс WG и делаем конфиг клиента.

![image](https://github.com/16Angeles/2024_2025-network_programming-k34202-islamov_s_s/blob/313e4360d77389df6ddc41bb1b43b1ce9293248f/lab1/1.jfif)

7. Заполняем строки: MTU оставляем как указано(при надобности можно поставить выше/ниже, зависимо от размера пакетов), ListenPort узнаём командой вывода файла /etc/wireguard/wg0.conf на сервере, ключи будут сгененрированы автоматически.
   
![image](https://github.com/16Angeles/2024_2025-network_programming-k34202-islamov_s_s/blob/313e4360d77389df6ddc41bb1b43b1ce9293248f/lab1/%D0%B8%D0%BD%D1%82%D1%8B.jfif)

8. Переходим во вторую вкладку, там создаём Peer - указываем только что созданный интерфейс, указываем публичный ключ сервера, его публичный IP, указанный ранее порт и сеть адресов, по которым будет идти подключение.

![image](https://github.com/16Angeles/2024_2025-network_programming-k34202-islamov_s_s/blob/7cf6a6c4bff085cc761fd651aca56bd9b25f8a23/lab1/%D0%BF%D0%B8%D1%80%D1%8B.jfif)

9. В настройке IP - Addresses указываем выбранную сеть и созданный интерфейс.

![image](https://github.com/16Angeles/2024_2025-network_programming-k34202-islamov_s_s/blob/5e16091b5094341fdb6f64b953a40387e27b9cc3/lab1/%D0%B0%D0%B4%D1%80%D0%B5%D1%81%D0%B0.png)

10. В настройке IP - Firewall создаём NAT Rule masquerade, Masquerade NAT позволяет преобразовывать несколько IP-адресов в другой одиночный IP-адрес. Можно использовать маскарадный NAT, чтобы скрыть один или несколько IP-адресов во внутренней сети за IP-адресом, который нужно сделать общедоступным.

![image](https://github.com/16Angeles/2024_2025-network_programming-k34202-islamov_s_s/blob/ae304f387d734ee7ccb81228b9b3e7f763934220/lab1/%D1%84%D0%B0%D0%B9%D1%80%D0%B2%D0%BE%D0%BB.png)

11. Теперь для проверки работоспособности запускаем ping к виртуальной машине по заданному IP адресу. Пинг идёт - следовательно, все настройки выполнены корректно.

![image](https://github.com/16Angeles/2024_2025-network_programming-k34202-islamov_s_s/blob/ae304f387d734ee7ccb81228b9b3e7f763934220/lab1/%D0%BF%D0%B8%D0%BD%D0%B3%D0%B8.jfif)

12. В результате получаем связь по заданной схеме из лабораторной работы. 

Выводы: При помощи WireGuard возможно настроить VPN туннель между виртуальной машиной с операционной системой RouterOS и удалённой виртуальной машиной, но только если вы отправляете пакеты из РФ в РФ, потому что к сожалению для иностранных ресурсов WG заблокирован. Для работы с RouterOS достаточно удобно использовать графический интерфейс WinBox, так как он значительно уменьшает время выполнения.
