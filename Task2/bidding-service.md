# Границы:
- определяет пользователей
- подбирает кандидатов в рекламу
# Зависимости:
- зависит от БД, модели данных в ней
# Модель данных

### subject - Внутренняя рекламная идентичность 

| Поле         | Тип       | Назначение                        |     |
| ------------ | --------- | --------------------------------- | --- |
| subject_id   | UUID      | Внутренний идентификатор субъекта |     |
| ubject_type  | ENUM      | Пользователь, устройство, сессия  |     |
| tatus        | ENUM      | Активен, заблокирован, удалён     |     |
| created_at   | TIMESTAMP | Время создания                    |     |
| last_seen_at | TIMESTAMP | Последняя активность              |     |

### subject_identifier Поиск субъекта по внешнему ID

| Поле                 | Тип       | Назначение              |
| -------------------- | --------- | ----------------------- |
| dentifier_id         | UUID      | Идентификатор записи    |
| subject_id           | UUID      | Ссылка на субъект       |
| identifier_type      | ENUM      | Тип идентификатора      |
| dentifier_value_hash | STRING    | Хеш значения            |
| source               | STRING    | Источник идентификатора |
| confidence           | DECIMAL   | Уверенность в связи     |
| valid_from           | TIMESTAMP | Начало действия         |
| valid_until          | TIMESTAMP | Окончание действия      |
| last_seen_at         | TIMESTAMP | Последнее использование |

### subject_profile Профиль пользователя

| Поле        | Тип       | Назначение             |
| ----------- | --------- | ---------------------- |
| subject_id  | UUID      | Идентификатор субъекта |
| attributes  | JSON      | Атрибуты профиля       |
| version     | INTEGER   | Версия профиля         |
| source      | STRING    | Источник данных        |
| updated_at  | TIMESTAMP | Время обновления       |
| valid_until | TIMESTAMP | Срок актуальности      |

### subject_attribute Атрибуты пользователя

| Поле            | Тип       | Назначение             |
| --------------- | --------- | ---------------------- |
| subject_id      | UUID      | Идентификатор субъекта |
| attribute_key   | STRING    | Название атрибута      |
| attribute_value | STRING    | Значение               |
| value_type      | ENUM      | Тип значения           |
| source          | STRING    | Источник               |
| updated_at      | TIMESTAMP | Время обновления       |
| valid_until     | TIMESTAMP | Срок актуальности      |

### segment Справочник сегментов

| Поле         | Тип              | Назначение                  |
| ------------ | ---------------- | --------------------------- |
| segment_id   | UUID или INTEGER | Идентификатор сегмента      |
| code         | STRING           | Машинный код                |
| name         | STRING           | Название                    |
| segment_type | ENUM             | Тип сегмента                |
| status       | ENUM             | Активен или выключен        |
| definition   | JSON             | Правила расчёта, если нужны |
| version      | INTEGER          | Версия                      |
| created_at   | TIMESTAMP        | Время создания              |
| updated_at   | TIMESTAMP        | Время изменения             |

### segment_membership Сегменты пользователя

| Поле         | Тип              | Назначение                  |
| ------------ | ---------------- | --------------------------- |
| segment_id   | UUID или INTEGER | Идентификатор сегмента      |
| code         | STRING           | Машинный код                |
| name         | STRING           | Название                    |
| segment_type | ENUM             | Тип сегмента                |
| status       | ENUM             | Активен или выключен        |
| definition   | JSON             | Правила расчёта, если нужны |
| version      | INTEGER          | Версия                      |
| created_at   | TIMESTAMP        | Время создания              |

### ad_candidate Рекламный кандидат

| Поле                | Тип       | Назначение                       |
| ------------------- | --------- | -------------------------------- |
| candidate_id        | UUID      | Идентификатор кандидата          |
| external_ad_id      | STRING    | ID рекламы во внешней системе    |
| placement_id        | STRING    | Место показа                     |
| candidate_type      | STRING    | Тип предложения или рекламы      |
| status              | ENUM      | Активен или выключен             |
| priority            | INTEGER   | Приоритет, если нужен            |
| targeting_policy_id | UUID      | Правила таргетинга               |
| payload             | JSON      | Данные, возвращаемые потребителю |
| start_at            | TIMESTAMP | Начало активности                |
| end_at              | TIMESTAMP | Окончание активности             |
| version             | INTEGER   | Версия данных                    |
| updated_at          | TIMESTAMP | Время обновления                 |

### candidate_placement Контекст размещения 

| Поле         | Тип     | Назначение                |
| ------------ | ------- | ------------------------- |
| candidate_id | UUID    | Кандидат                  |
| placement_id | STRING  | Место показа              |
| included     | BOOLEAN | Разрешение или исключение |

### targeting_policy Правила таргетинга

| Поле                 | Тип       | Назначение             |
| -------------------- | --------- | ---------------------- |
| `targeting_policy_id | UUID      | Идентификатор политики |
| definition           | JSON      | Декларативные правила  |
| status               | ENUM      | Статус политики        |
| version              | INTEGER   | Версия                 |
| created_at           | TIMESTAMP | Время создания         |
| updated_at           | TIMESTAMP | Время обновления       |
