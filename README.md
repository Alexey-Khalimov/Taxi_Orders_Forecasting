# Taxi Orders Forecasting

## Описание проекта
Компания такси собрала исторические данные о заказах такси в аэропортах. Для привлечения большего числа водителей в периоды пиковой нагрузки требуется спрогнозировать количество заказов на следующий час. Основная цель проекта — построить модель предсказания количества заказов такси с метрикой RMSE не более 48 на тестовой выборке.

## Этапы выполнения проекта

### 1. Подготовка данных
- **Загрузка и предварительная обработка:**
  - Данные загружены из файла `/datasets/taxi.csv`.
  - Проверены на наличие пропусков, дубликатов и некорректных значений.
  - Выполнена агрегация данных с ресемплированием по часу для формирования временного ряда.
- **Создание признаков:**
  - Добавлены временные признаки, такие как час, день недели, выходной/рабочий день, чтобы учесть временные паттерны.
  - Выявлены сезонные тренды, такие как утренние и вечерние пики спроса.
  - Созданы лаговые признаки для учёта зависимости текущего спроса от предыдущих значений.
  - Рассчитаны скользящие средние для сглаживания данных.

### 2. Анализ данных
- **Исследование временных рядов:**
  - Проведён анализ трендов и сезонности в данных.
  - Построены графики временного ряда для визуализации изменений количества заказов во времени.
  - Выявлены пики и провалы в заказах, связанные с временными факторами (например, ночью и в будние дни).
- **Проверка статистических свойств:**
  - Проверено наличие стационарности временного ряда с помощью теста Дики-Фуллера.
  - Проанализированы автокорреляция и частичная автокорреляция для определения важности лагов.

### 3. Обучение моделей
- **Разделение данных:**
  - Данные разделены на обучающую и тестовую выборки (10% данных отведено под тест).
- **Модели:**
  - Обучены несколько моделей, включая:
    - Линейная регрессия.
    - Градиентный бустинг (CatBoost, XGBoost).
  - Для каждой модели выполнен подбор гиперпараметров с использованием кросс-валидации.
- **Оценка моделей:**
  - Основная метрика — RMSE. Дополнительно рассчитаны MAE и R² для более глубокого анализа точности.
  - Проверена значимость добавленных признаков.

### 4. Оценка результатов
- На тестовой выборке модели показали следующие результаты:
  - Лучшая модель — CatBoost с RMSE = 46.8.
  - Модель успешно предсказала временные пики и провалы спроса, обеспечив точность на уровне бизнес-целей.
- Построены графики фактических и предсказанных значений для визуального анализа.

### 5. Выводы
- Лучшая модель соответствует требованиям бизнеса по точности (RMSE < 48).
- Установлено, что временные признаки и лаговые переменные оказывают значительное влияние на точность предсказаний.
- Разработанный инструмент позволяет компании «Чётенькое такси» заранее планировать работу водителей, улучшая баланс спроса и предложения в пиковые часы.

## Использование
- Для выполнения проекта необходимо:
  1. Установить Python и необходимые библиотеки (`pandas`, `numpy`, `scikit-learn`, `catboost`, `matplotlib`, `etna`).
  2. Скачать данные и поместить их в директорию `/datasets/taxi.csv`.
  3. Запустить Jupyter Notebook или Python-скрипт с основным кодом.
- Модель обучена и готова к применению на новых данных в реальном времени.

## Автор
Проект выполнен в рамках анализа данных и машинного обучения.