# Диаграммы

## Диаграмма последовательности

Диаграмма показывает выполнение UC-01 — проверку сообщения на спам.

```mermaid
sequenceDiagram
    actor User as Пользователь
    participant App as Приложение
    participant Model as ML-модель

    User->>App: Ввести текст и нажать «Проверить»
    App->>App: Проверить наличие текста

    alt Текст пустой
        App-->>User: Показать просьбу ввести сообщение
    else Текст заполнен
        App->>Model: Передать текст для классификации
        alt Обработка выполнена
            Model-->>App: Вернуть результат классификации
            App-->>User: Показать «Спам» или «Обычное сообщение»
        else Ошибка обработки
            Model-->>App: Сообщить об ошибке
            App-->>User: Предложить повторить проверку
        end
    end
```

## Диаграмма классов

Диаграмма описывает основные сущности системы:

- SpamDetectionApp — приложение, принимающее текст пользователя;
- Message — проверяемое сообщение;
- SpamClassifier — ML-компонент для определения спама;
- ClassificationResult — результат классификации.

```mermaid
classDiagram
    class SpamDetectionApp {
        +checkMessage(text)
        +showResult(result)
        +showError(message)
    }

    class Message {
        +string text
    }

    class SpamClassifier {
        +predict(message) ClassificationResult
    }

    class ClassificationResult {
        +string label
    }

    SpamDetectionApp ..> Message : создаёт
    SpamDetectionApp ..> SpamClassifier : вызывает
    SpamDetectionApp ..> ClassificationResult : отображает
    SpamClassifier ..> Message : анализирует
    SpamClassifier ..> ClassificationResult : возвращает
```