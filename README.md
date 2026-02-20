# Домашнее задание к занятию "`ELK`" - `Дорожкин Артем`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1. Elasticsearch

---

Установите и запустите Elasticsearch, после чего поменяйте параметр cluster_name на случайный. 

*Приведите скриншот команды 'curl -X GET 'localhost:9200/_cluster/health?pretty', сделанной на сервере с установленным Elasticsearch. Где будет виден нестандартный cluster_name*.

### Решение 1.

<img width="658" height="236" alt="image" src="https://github.com/user-attachments/assets/e9e6f486-365c-42b8-b11b-8fb844090b4e" />

---

### Задание 2. Kibana

Установите и запустите Kibana.

*Приведите скриншот интерфейса Kibana на странице http://<ip вашего сервера>:5601/app/dev_tools#/console, где будет выполнен запрос GET /_cluster/health?pretty*.

### Решение 2.


<img width="897" height="383" alt="24245" src="https://github.com/user-attachments/assets/53a40479-377a-4875-9ba6-f969a2508ef8" />

---

### Задание 3. Logstash

Установить и запустить Logstash и Nginx. С помощью Logstash отправить access-лог nginx в Elasticsearch.

Приведите скриншот интерфейса kibana, на котором видны логи nginx.
___
**Ответ**



<img width="1919" height="819" alt="image" src="https://github.com/user-attachments/assets/32a518ce-b4b1-4044-9784-c1c7795a663a" />


Установка nginx.  
```
sudo apt install nginx
```
Установка logstash.  
```
sudo apt install ./logstash-8.12.2-amd64.deb 
```
Создать файл конфигурации по адресу /etc/logstash/conf.d/logstash.conf.

Далее настроить поставку access-лога nginx в elasticsearch:  
```
# Читаем файл
input {
  file {
    path => ["/var/log/nginx/access.log"]
    start_position => "beginning"
  }
}
# Извлекаем данные из событий
filter {
  grok {
    match => { "message" => "\[%{TIMESTAMP_ISO8601:timestamp}\]\[%{DATA:severity}%{SPACE}\]\[%{DATA:source}%{SPACE}\]%{SPACE}%{GREEDYDATA:message}" }
    overwrite => [ "message" ]
  }
}
# Сохраняем все в Elasticsearch
output {
  elasticsearch {
    hosts => ["http://localhost:9200"]
    index => "nginx-logs-%{+YYYY.MM}"
  }
}
```
Запуск службы logstash.  
```
sudo systemctl daemon-reload  
sudo systemctl enable logstash.service   
sudo systemctl start logstash.service  
sudo systemctl status logstash.service
```
Создать данные для просмотра в kibana.  
Маршрут: Management > stack management	> kibana > data view > Create data view!

_______________________________

<img width="1362" height="547" alt="image" src="https://github.com/user-attachments/assets/fbeaa4c0-440e-4f7a-a102-ac3795a08f81" />



<img width="1366" height="547" alt="image" src="https://github.com/user-attachments/assets/778a96c9-943b-4194-9b41-7000d58b6b0c" />

<img width="1366" height="547" alt="image" src="https://github.com/user-attachments/assets/07336819-6ba2-4461-8ba1-a76502229d7b" />



четвертое

<img width="1366" height="538" alt="image" src="https://github.com/user-attachments/assets/7601832e-75f6-4088-af9d-ad484840eef4" />


_____________________________



```


### Задание 4. Filebeat

Установить и запустить Filebeat. Переключить поставку логов Nginx с Logstash на Filebeat.

Приведите скриншот интерфейса kibana, на котором видны логи nginx, которые были отправлены через Filebeat.

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`
