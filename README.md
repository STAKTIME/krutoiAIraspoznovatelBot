# krutoiAIraspoznovatelBot 🔩🤖

Telegram-бот, который распознаёт тип металла по фотографии с помощью ИИ-модели. Весь проект реализован в **одном Google Colab ноутбуке**.

Бот определяет один из следующих материалов:
- 🟫 **Карбон**
- 🟠 **Медь**
- 🟡 **Латунь**
- ⚙️ **Железо**

## 📌 Как это работает

1. Пользователь отправляет боту фото в Telegram.
2. Бот скачивает фото и запускает распознавание в фоновом потоке (пока идёт обработка — показывает анимацию "Понял, принял, обрабатываю...").
3. Модель (обученная в **Teachable Machine**, формат Keras) классифицирует изображение по 4 классам металлов.
4. Бот присылает пользователю результат распознавания.

## 🛠️ Технологии

- [pyTelegramBotAPI](https://github.com/eternnoir/pyTelegramBotAPI) (`telebot`) — взаимодействие с Telegram
- `tf-keras` — загрузка и инференс модели
- `Pillow` (PIL) — предобработка изображений
- `threading` — неблокирующая обработка фото с анимацией ожидания
- Модель обучена в [Google Teachable Machine](https://teachablemachine.withgoogle.com/) и экспортирована в формате Keras (`keras_model.h5` + `labels.txt`)

## 📁 Структура репозитория

```
krutoiAIraspoznovatelBot/
└── Боть_металлы_распозноющъ.ipynb   # весь код бота (Google Colab)
```

## 🚀 Запуск

Проект запускается прямо в Google Colab:

1. Открой ноутбук `Боть_металлы_распозноющъ.ipynb` в [Google Colab](https://colab.research.google.com/github/STAKTIME/krutoiAIraspoznovatelBot/blob/main/%D0%91%D0%BE%D1%82%D1%8C_%D0%BC%D0%B5%D1%82%D0%B0%D0%BB%D0%BB%D1%8B_%D1%80%D0%B0%D1%81%D0%BF%D0%BE%D0%B7%D0%BD%D0%BE%D1%8E%D1%89%D1%8A.ipynb) (кнопка "Open in Colab" есть в самом файле).
2. Загрузи в среду выполнения Colab архив с обученной моделью **`converted_keras.zip`** (должен содержать `keras_model.h5` и `labels.txt`) — например, через панель Files слева.
3. Впиши свой Telegram-токен бота в переменную `API_TOKEN` в соответствующей ячейке:
```python
API_TOKEN = 'ТВОЙ_ТОКЕН_ОТ_BOTFATHER'
```
4. Выполни все ячейки ноутбука по порядку (сверху вниз):
   - установка `pytelegrambotapi`
   - распаковка `converted_keras.zip`
   - установка `tf-keras` и `h5py`
   - запуск функции `recognizer()`
   - запуск бота (`bot.polling()`)
5. Бот готов принимать фото в Telegram.

⚠️ **Важно:** Colab-сессия работает только пока открыта вкладка/выполняется ноутбук. Для постоянной работы бота потребуется развернуть код на сервере (VPS, Railway, Render и т.д.) вне Colab.

## 🧠 Модель

Модель классификации создана в Google Teachable Machine и обучена на изображениях 4 классов металлов: карбон, медь, латунь, железо. Для замены/дообучения модели создайте новый проект на [teachablemachine.withgoogle.com](https://teachablemachine.withgoogle.com/), обучите классификатор изображений на своих данных и экспортируйте его в формате **Tensorflow → Keras**, получив `converted_keras.zip`.

## 🖼️ Пример использования

```
Пользователь отправляет фото → 
Бот: "Понял, принял, обрабатываю..." →
Бот: "Результат: Латунь"
```

## 🔑 Получение токена Telegram-бота

1. Напиши [@BotFather](https://t.me/BotFather) в Telegram
2. Команда `/newbot`, следуй инструкциям
3. Скопируй выданный токен в переменную `API_TOKEN`

## 📄 Лицензия

Copyright © 2026 ООО «krutoiAIraspoznovatelBot». All rights reserved

---


