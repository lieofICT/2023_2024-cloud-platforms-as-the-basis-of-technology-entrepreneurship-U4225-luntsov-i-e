<div align="center">

University: [ITMO University](https://itmo.ru/ru/) 

Faculty: [FICT](https://fict.itmo.ru)

Course: [Cloud platforms as the basis of technology entrepreneurship](https://itmo-ict-faculty.github.io/cloud-platforms-as-the-basis-of-technology-entrepreneurship/)

Year: 2024/2025

Group: U4225

Author: Luntsov Ilya Evgenevich

Lab: Lab1

Date of create: 06.11.2024

Date of finished: 06.11.2024

</div>

---

В ходе лабораторной работы была выполнена настройка доступа, создание виртуальной машины в Google Cloud Platform и проверка влияния ролей на доступ к Cloud Storage.

Подробнее раскажу далее.

### Шаг 1: Создание Service Account с ролью Storage Admin

1. Перешел в раздел **IAM & Admin** > **Service Accounts**.
2. Создал новый service account с именем `iluntsov-sa-lab1`.
3. Назначил роль **Storage Admin**.

![Создание Service Account - Часть 1](Шаг1_(1).png)
![Создание Service Account - Часть 2](Шаг1_(2).png)

### Шаг 2: Создание виртуальной машины в Google Cloud

1. Перешел в раздел **Compute Engine** > **VM instances**.
2. Создал новую виртуальную машину с именем `iluntsov-vm-lab1`.
3. Выбрал тип машины **e2-micro** и включил режим **spot**.

![Создание VM - Часть 1](Шаг2_(1).png)
![Создание VM - Часть 2](Шаг2_(2).png)
![Создание VM - Часть 3](Шаг2_(3).png)

### Шаг 3: Копирование файлов из Cloud Storage в VM

1. Подключился к виртуальной машине через **SSH**.
2. Использовал команду `gsutil cp` для копирования файлов из бакета `lab1-bucket-itmo` в локальную папку на VM.
3. Проверил наличие файлов командой `ls -lah`.

```bash
gsutil cp gs://lab1-bucket-itmo/* ~/lab1-files
ls -lah ~/lab1-files
```

![Копирование файлов - Часть 1](Шаг3_(1).png)
![Копирование файлов - Часть 2](Шаг3_(2).png)

### Шаг 4: Изменение роли Service Account на Compute Viewer

1. Перешел в **IAM & Admin** > **IAM**.
2. Изменил роль service account `iluntsov-sa-lab1` с **Storage Admin** на **Compute Viewer**.
3. Повторил попытку копирования файлов и убедился, что доступ ограничен.

![Изменение роли - Часть 1](Шаг4_(1).png)
![Изменение роли - Часть 2](Шаг4_(1).png)

### Выводы

Изменение роли с **Storage Admin** на **Compute Viewer** ограничивает доступ к Cloud Storage, из-за чего не получилось копировать файлы. Для работы с бакетами необходимы права, включенные в роли, такие как **Storage Admin**.
