# Write own Netflix 👹

Информация о каждом сервисе:

[Content-service](Write%20own%20Netflix%20%F0%9F%91%B9%20137f09a12cfb8099b9eaf0bf320e51a6/Content-service%2013bf09a12cfb80ab850cda035344b79b.md)

[Rating Service](Write%20own%20Netflix%20%F0%9F%91%B9%20137f09a12cfb8099b9eaf0bf320e51a6/Rating%20Service%2013bf09a12cfb8087a525f1ae47e80e07.md)

**Техническое задание:**

Разработка микросервисного приложения для потокового воспроизведения видео, аналогичного Netflix. Система должна включать несколько микросервисов, которые будут взаимодействовать между собой для обеспечения аутентификации, управления контентом, персонализированных рекомендаций, подписки и уведомлений.

**Цели:**

```
•	Разработать архитектуру микросервисов.
•	Обеспечить аутентификацию и авторизацию пользователей с помощью JWT.
•	Реализовать функционал управления контентом (фильмы, сериалы, и т.д.).
•	Реализовать механизм подписки и проверку прав доступа.
•	Разработать систему уведомлений для пользователей.
•	Обеспечить поиск по контенту с возможностью фильтрации.
```

**Технологии**

```java
•	Язык программирования: Java 17,21 (Spring Boot для микросервисов).
•	База данных: PostgreSQL или MongoDB для хранения данных пользователей, контента, подписок и оценок.
•	API Gateway: Spring Cloud Gateway или Nginx.
•	JWT для аутентификации и авторизации.
•	Redis для кэширования и повышения производительности.
•	Kafka для взаимодейтсвия микро-сервсисов
•	Docker и Docker Compose для контейнеризации и развертывания всех сервисов.
• Подробнее:
	 - Liquibase
	 - Mapstruct
	 - Lombok
	 - Swagger
	 - Spring Retry
	 - Resilience4j
	 - Spring Security, Config-Server/Client, Cloud, Data, Mvc, 
	 - Testcontainers, MockMvc, WireMock, JUnit, Mockito
```

- **Микро-сервисы:**
    
    Для создания приложения, похожего на Netflix, на базе микросервисной архитектуры можно предложить следующий набор сервисов:
    
    1.	**Gateway (API Gateway)**
    
    •	Этот микросервис будет служить точкой входа для всех запросов пользователей. Он направляет запросы к соответствующим микросервисам (например, аутентификации или контенту) и может реализовывать балансировку нагрузки, кэширование, а также обработку маршрутов.
    
    2.	**Auth-Service (Сервис аутентификации и авторизации)**
    
    •	Отвечает за регистрацию, вход пользователей и управление их сессиями. Может использовать JWT (JSON Web Tokens) для выдачи токенов при успешной аутентификации. Он будет взаимодействовать с Gateway для проверки токенов и с другими сервисами для авторизации доступа к данным.
    
    3.	**User-Service (Сервис пользователей)**
    
    •	Этот сервис хранит и управляет данными пользователей, такими как профиль, настройки и предпочтения. Он взаимодействует с Auth-Service для обеспечения безопасности и с другими сервисами для персонализированного контента.
    
    4.	**Content-Service (Сервис контента)**
    
    •	Управляет информацией о фильмах, сериалах и других медиа-ресурсах. Содержит метаданные (жанр, актеры, режиссеры и т.д.) и может взаимодействовать с базой данных для получения подробной информации. Этот сервис отправляет метаданные через API Gateway.
    
    5.	**Recommendation-Service (Сервис рекомендаций)**
    
    •	Генерирует рекомендации для пользователей на основе их истории просмотров, оценок и предпочтений. Этот сервис взаимодействует с User-Service для получения данных о пользователях и с Content-Service для получения информации о контенте.
    
    6.	**Subscription-Service (Сервис подписки)**
    
    •	Управляет подписками пользователей, проверяет их статус и различные уровни доступа (например, стандартный, премиум). Он взаимодействует с User-Service и Gateway, чтобы определять доступ пользователя к контенту.
    
    7.	**Rating-Service (Сервис оценок)**
    
    •	Позволяет пользователям оценивать фильмы и сериалы. Оценки можно использовать для улучшения рекомендаций и отображения статистики. Взаимодействует с User-Service и Content-Service для получения данных о пользователях и контенте.
    
    8.	**Search-Service (Сервис поиска)******
    
    •	Обеспечивает функциональность поиска контента по ключевым словам, жанрам и другим фильтрам. Может использовать Elasticsearch или аналогичные технологии. Взаимодействует с Content-Service для получения информации о контенте.
    
    9.	**Notification-Service (Сервис уведомлений)**
    
    •	Отправляет уведомления пользователям, например, о новых релизах, изменениях в подписке или специальных предложениях. Он будет взаимодействовать с User-Service для определения целевой аудитории и с другими сервисами для получения информации о новых событиях.
    
    **Взаимодействие сервисов:**
    
    •	**Gateway** — это единственная точка входа, которая маршрутизирует запросы между сервисами. Все запросы сначала проходят через него.
    
    •	**Auth-Service** проверяет JWT, выданные при аутентификации, и передает их в другие сервисы для обеспечения безопасности.
    
    •	**User-Service** взаимодействует с большинством других сервисов для управления данными пользователей.
    
    •	**Content-Service** и **Recommendation-Service** могут обмениваться данными о контенте и предпочтениях пользователей для улучшения качества рекомендаций.
    
    •	**Subscription-Service** будет определять доступ пользователя к контенту на основе их подписки.
    
    •	**Search-Service** и **Rating-Service** будут активно взаимодействовать с **Content-Service** для получения метаданных и оценок контента.
    
    •	**Notification-Service** будет взаимодействовать с **User-Service** для отправки уведомлений.
    
    Такая архитектура позволяет гибко масштабировать приложение, добавлять новые функциональные блоки и упрощать управление безопасностью и доступом.
    
- **Функциональные требования:**
    
    Вот пример набора **endpoints** для каждого из микросервисов в вашем приложении:
    
    **1. Gateway (API Gateway)**
    
    •	**GET /** — проверка доступности сервиса.
    
    •	**POST /login** — перенаправление на сервис аутентификации.
    
    •	**POST /register** — перенаправление на сервис регистрации пользователя.
    
    •	**GET /content** — перенаправление на сервис контента для получения списка контента.
    
    •	**GET /content/{id}** — перенаправление на сервис контента для получения подробной информации о контенте.
    
    •	**GET /search** — перенаправление на сервис поиска контента.
    
    •	**GET /recommendations** — перенаправление на сервис рекомендаций для получения рекомендаций.
    
    **2. Auth-Service**
    
    •	**POST /login** — аутентификация пользователя. Возвращает JWT.
    
    •	**POST /register** — регистрация нового пользователя.
    
    •	**POST /logout** — завершение сессии пользователя.
    
    •	**GET /user/{id}** — получение данных пользователя по ID.
    
    •	**POST /refresh-token** — обновление истекшего JWT токена.
    
    **3. User-Service**
    
    •	**GET /user/{id}** — получение данных пользователя.
    
    •	**PUT /user/{id}** — обновление данных пользователя.
    
    •	**GET /user/{id}/preferences** — получение предпочтений пользователя (жанры, языки и т. д.).
    
    •	**PUT /user/{id}/preferences** — обновление предпочтений пользователя.
    
    •	**GET /user/{id}/history** — получение истории просмотров пользователя.
    
    •	**POST /user/{id}/history** — добавление фильма/сериала в историю просмотров пользователя.
    
    **4. Content-Service**
    
    •	**GET /content** — получение списка контента (фильмов, сериалов).
    
    •	**GET /content/{id}** — получение подробной информации о контенте (например, жанр, описание, актеры).
    
    •	**POST /content** — добавление нового контента (доступно только администраторам).
    
    •	**PUT /content/{id}** — обновление информации о контенте (доступно только администраторам).
    
    •	**DELETE /content/{id}** — удаление контента (доступно только администраторам).
    
    **5. Recommendation-Service**
    
    •	**GET /recommendations/{userId}** — получение персонализированных рекомендаций для пользователя.
    
    •	**POST /recommendations** — обновление рекомендаций для всех пользователей на основе нового контента или истории.
    
    •	**GET /recommendations/top** — получение популярных рекомендаций для всех пользователей.
    
    **6. Subscription-Service**
    
    •	**GET /subscriptions/{userId}** — получение текущего статуса подписки пользователя.
    
    •	**POST /subscriptions/{userId}** — оформление подписки.
    
    •	**PUT /subscriptions/{userId}** — изменение подписки пользователя (например, переход на более дорогой тариф).
    
    •	**DELETE /subscriptions/{userId}** — отмена подписки пользователя.
    
    **7. Rating-Service**
    
    •	**POST /rating/{contentId}** — оценка контента пользователем.
    
    •	**GET /rating/{contentId}** — получение средней оценки контента.
    
    •	**GET /ratings/{userId}** — получение всех оценок пользователя.
    
    **8. Search-Service*****
    
    •	**GET /search** — поиск контента по ключевым словам.
    
    •	**GET /search/filters** — получение доступных фильтров для поиска (жанры, рейтинг и т. д.).
    
    •	**GET /search/{query}** — поиск контента по запросу (например, название или актер).
    
    **10. Notification-Service**
    
    •	**POST /notifications/send** — отправка уведомлений пользователю.
    
    •	**GET /notifications/{userId}** — получение всех уведомлений пользователя.
    
    •	**POST /notifications/subscribe** — подписка пользователя на уведомления.
    
    •	**POST /notifications/unsubscribe** — отмена подписки на уведомления.
    
    **Важные моменты для взаимодействия сервисов:**
    
    •	**API Gateway** будет отправлять запросы к соответствующим микросервисам (например, в сервис аутентификации, получения контента или рекомендаций).
    
    •	**Auth-Service** будет работать с JWT для авторизации пользователя, встраивать токены в заголовки запросов.
    
    •	**User-Service** будет обеспечивать персонализацию и хранение данных о пользователях, а также обрабатывать их предпочтения и историю.
    
    •	**Content-Service** и **Recommendation-Service** будут использовать REST API для обмена данными о контенте и рекомендациях.
    
    •	**Subscription-Service** будет отслеживать статус подписки пользователя и передавать данные в другие сервисы (например, в Streaming-Service для проверки доступа к контенту).
    
    Такой набор endpoints обеспечивает гибкое взаимодействие между сервисами и возможность масштабирования системы.
