
### **1. UFW (Uncomplicated Firewall)**

| **Команда**                           | **Описание**                                  |
| ------------------------------------- | --------------------------------------------- |
| ```sudo ufw status```                 | Проверить статус фаервола UFW.                |
| ```sudo ufw enable```                 | Включить UFW.                                 |
| ```sudo ufw disable```                | Отключить UFW.                                |
| ```sudo ufw allow 22/tcp```           | Разрешить порт 22 для TCP (SSH).              |
| ```sudo ufw deny 22/tcp```            | Закрыть порт 22 для TCP.                      |
| ```sudo ufw allow 443/tcp```          | Разрешить порт 443 для HTTPS.                 |
| ```sudo ufw status verbose```         | Подробный вывод состояния UFW.                |
| ```sudo ufw delete allow 22/tcp```    | Удалить правило для порта 22.                 |
| ```sudo ufw default deny incoming```  | Блокировать входящие соединения по умолчанию. |
| ```sudo ufw default allow outgoing``` | Разрешить исходящие соединения по умолчанию.  |

---
### **1.1 iptables (Фаервол)**

| **Команда**                                                                                  | **Описание**                                           |
| -------------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| ```sudo iptables -L```                                                                       | Просмотр текущих правил фаервола.                      |
| ```sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT```                                     | Открыть порт 22 (SSH).                                 |
| ```sudo iptables -A INPUT -p tcp --dport 22 -j REJECT```                                     | Закрыть порт 22 (SSH).                                 |
| ```sudo iptables -D INPUT -p tcp --dport 22 -j ACCEPT```                                     | Удалить правило для порта 22.                          |
| ```sudo iptables-save > /etc/iptables/rules.v4```                                            | Сохранить текущие правила фаервола.                    |
| ```sudo ss -tuln```                                                                          | Просмотр открытых портов и активных соединений.        |
| ```sudo iptables -A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/s -j ACCEPT``` | Разрешить ICMP (ping) с ограничением 1 пинг в секунду. |
| ```sudo iptables -A INPUT -p icmp -j REJECT```                                               | Отключить ICMP (ping).                                 |
| ```sudo iptables -F```                                                                       | Сбросить все правила фаервола.                         |


---
### **2. Fail2Ban**

| **Команда**                                                | **Описание**                                                                                        |
| ---------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| ```sudo systemctl status fail2ban```                       | Проверить статус службы Fail2Ban.                                                                   |
| ```sudo systemctl restart fail2ban```                      | Перезапустить Fail2Ban.                                                                             |
| ```sudo fail2ban-client status```                          | Просмотр статуса всех тюрем (jails).                                                                |
| ```sudo fail2ban-client status sshd```                     | Проверить статус фильтра **sshd** (заблокированные IP и другие данные).                             |
| ```sudo fail2ban-client set sshd banip <IP-адрес>```       | Заблокировать IP-адрес для **sshd** (например, 192.168.1.1).                                        |
| ```sudo fail2ban-client set sshd unbanip <IP-адрес>```     | Разблокировать IP-адрес для **sshd**.                                                               |
| ```sudo fail2ban-client set <filter> unbanip <IP-адрес>``` | Разблокировать IP-адрес для выбранного фильтра (например, **apache**).                              |
| ```sudo journalctl -u fail2ban```                          | Просмотр логов Fail2Ban для ошибок и событий.                                                       |
| ```sudo nano /etc/fail2ban/jail.local```                   | Редактирование конфигурации Fail2Ban (например, настройка максимальных попыток входа для **sshd**). |
| ```sudo fail2ban-client reload <jail-name>```              | Перезагрузить настройки конкретного фильтра (например, **sshd**).                                   |


sudo ss -tuln | grep :80

проверить порт