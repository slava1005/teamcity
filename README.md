## Домашнее задание к занятию 11 «Teamcity»
### Подготовка к выполнению
В Yandex Cloud создайте новый инстанс (4CPU4RAM) на основе образа jetbrains/teamcity-server.

![img_1](https://github.com/user-attachments/assets/acb7ee84-ed85-48d2-8c30-efbf36dd2fe9)

Дождитесь запуска teamcity, выполните первоначальную настройку.

![img_2](https://github.com/user-attachments/assets/799928e5-a74f-4770-b1a6-5ff76fda9855)

Создайте ещё один инстанс (2CPU4RAM) на основе образа jetbrains/teamcity-agent. Пропишите к нему переменную окружения SERVER_URL: "http://<teamcity_url>:8111".

![img_3](https://github.com/user-attachments/assets/a5adcc73-b7f3-4bbf-9e6b-8b968abd5a25)

Авторизуйте агент.
Сделайте fork репозитория.

![fork](https://github.com/user-attachments/assets/c52e0f1c-dac3-4425-b0f6-bee8f1c92fac)

Создайте VM (2CPU4RAM) и запустите playbook.


### Основная часть
1. Создайте новый проект в teamcity на основе fork.

![img_4](https://github.com/user-attachments/assets/162222b7-fc48-457a-ab7a-f908cabdd21c)

2. Сделайте autodetect конфигурации.

![img_5](https://github.com/user-attachments/assets/f0416fe1-0b75-4808-903d-1ec482447b7e)

3. Сохраните необходимые шаги, запустите первую сборку master.

![img_6](https://github.com/user-attachments/assets/b0800799-c5c9-4f8b-ac54-c568c65881d7)

4. Поменяйте условия сборки: если сборка по ветке master, то должен происходит mvn clean deploy, иначе mvn clean test.

![img_7](https://github.com/user-attachments/assets/a31f38f2-f7dd-4d37-a5c7-17d7cf6d3b8e)

5. Для deploy будет необходимо загрузить settings.xml в набор конфигураций maven у teamcity, предварительно записав туда креды для подключения к nexus.

![img_8](https://github.com/user-attachments/assets/6d15635e-0976-4fd1-be4d-f67f75424d80)

6. В pom.xml репозитория изменил начальную версию и адрес nexus, запушил изменения.
7. Запустите сборку по master, убедитесь, что всё прошло успешно и артефакт появился в nexus.

![img_9](https://github.com/user-attachments/assets/599e1107-9f26-4aca-bbb7-0d5394ae037b)

8. Мигрируйте build configuration в репозиторий.

![img_10](https://github.com/user-attachments/assets/a1d1b23d-7c26-4492-888b-644492ce85b4)

9. Создайте отдельную ветку feature/add_reply в репозитории.

![img_11](https://github.com/user-attachments/assets/b29178ad-f62e-4b36-a58c-aa9aa6a9d33f)

10. Напишите новый метод для класса Welcomer: метод должен возвращать произвольную реплику, содержащую слово hunter.

![img_12](https://github.com/user-attachments/assets/ff3a559f-21da-481f-b79e-906fdbd1b1e4)

11. Дополните тест для нового метода на поиск слова hunter в новой реплике.

![img_13](https://github.com/user-attachments/assets/538792fb-41c1-4d4d-bafe-50021aabfa56)

12. Сделайте push всех изменений в новую ветку репозитория.

![img_14](https://github.com/user-attachments/assets/924c7c4c-98dd-46e7-8793-6a2a508d0716)

13. Убедитесь, что сборка самостоятельно запустилась, тесты прошли успешно.

![img_15](https://github.com/user-attachments/assets/0279ea71-69f4-4bd6-a588-7573fe0325d7)

14. Вносим изменения из произвольной ветки feature/add_reply в master через Merge.
15. Был собранный артефакт в сборке по ветке master, поэтому сборка не прошла.
Чтобы выполнить задачу есть 3 варианта:
- Изменить версию артефакта в pom.xml.
- Настроить Nexus на принятия релизных артефактов для данного репозиторя, то есть разрешить обновлять артефакты.
- Использовать снапшоты вместо релизов.
Думаю проще измененить версию артефакта в pom.xml.

16. Наша конфигурация уже настроена на сборку jar.
17. Проводим повторную сборку мастера, убеждаемся, что сборка прошла успешно и артефакты собраны.

![img_16_2](https://github.com/user-attachments/assets/70362e1d-78a1-4e30-8561-99a7b7510fa8)

Версия 0.0.2 на месте

![img_17_1](https://github.com/user-attachments/assets/bc06475c-1a5d-4296-bd06-f236a8691c80)

18. Проверяем, что конфигурация в репозитории содержит все настройки конфигурации из teamcity.

![img_18_1](https://github.com/user-attachments/assets/e423f716-461b-4ec4-8249-4c9cedebd69f)


