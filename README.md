# Задание 1
Разделить проект Mesto на несколько микрофронтендов.
Определить для этого фреймворк, — [Module Federation](https://webpack.js.org/concepts/module-federation/) или [Single SPA](https://single-spa.js.org/docs/getting-started-overview/).

## Уровень 1. Проектирование
- *TODO-1: Выбрать фреймворк для создания микрофронтендов.*
- *TODO-2: Описать решение.*

### ✅ Solution

#### Decision
Для проекта Mesto и поставленной задачи оптимален **Module Federation**.

#### Arguments
1. Module Federation позволяет постепенно разделить уже существующее монолитное приложение на отдельные части. Это удобно в данном конкретном случае, так как **уже есть готовый проект**.
2. Module Federation позволяет независимым командам **разрабатывать отдельные микрофронтенды параллельно**. Легко интегрируется в проекты на основе популярных фреймворков вроде React, Vue или Angular.
3. Module Federation подходит для **шеринга общих UI-компонентов и библиотек между микрофронтендами**, сокращая повторяющийся код и облегчая сопровождение решения.
4. Субъективно, посмотрев документацию, данный фреймворк кажется **более простым в плане освоения и применения** в данном конкретном случае.

## Уровень 2. Планирование изменений
- *TODO-3: Создать новые структуры проекта для каждого микрофронтенда.*
- *TODO-4: Перенести выбранные компоненты, стили и утилиты в соответствующие новые структуры.*
- *TODO-5: Описать компоненты, модули и запуск. А также обосновать своё решение — написать, почему использовали именно этот подход и разделили фронтенд на такие микрофронтенды.*

### ✅ Solution

#### Domain-Driven Design (DDD) для разбиения

Проанализировав бизнес-логику монолитного решения, выделены следующие микрофронтенды:

- `auth-microfrontend` – модуль для аутентификации
- `profile-microfrontend` – модуль для работы с профилем пользователя
- `photo-microfrontend` – модуль для работы с фотографиями
- `host-microfrontend` – основное приложение (динамически загружает 3 вышеперечисленных модуля)

#### Новая структура проекта (включая каждый микрофронтенд)

```
/auth-microfrontend
  /src
    /components
      Login.js               // Компонент входа пользователя
      Register.js            // Компонент регистрации пользователя
    /styles
      /login
        login.css            // Стили для компонента входа
      /auth-form
        auth-form.css        // Стили для компонента аутентификации      
    /utils
      auth.js                // Утилиты для аутентификации
    index.js                 // Точка входа микрофронтенда
  package.json               // Зависимости и скрипты микрофронтенда
  webpack.config.js
/profile-microfrontend
  /src
    /components
      EditAvatarPopup.js     // Компонент редактирования аватара пользователя
      EditProfilePopup.js    // Компонент редактирования профиля пользователя
      PopupWithForm.js       // Компонент диалогового окна сохранения
    /contexts
      CurrentUserContext.js  // Контекст
    /styles
      /popup
        popup.css            // Стили для компонента окна сохранения
      /profile
        profile.css          // Стили для компонента профиля пользователя
    index.js                 // Точка входа микрофронтенда
  package.json               // Зависимости и скрипты микрофронтенда
  webpack.config.js
/photo-microfrontend
  /src
    /components
      AddPlacePopup.js       // Компонент добавления фото
      Card.js                // Компонент карточки с изображением
      ImagePopup.js          // Компонент показа фото
      PopupWithForm.js       // Компонент диалогового окна сохранения
    /contexts
      CurrentUserContext.js  // Контекст
    /styles
      /card
        card.css             // Стили для компонента карточки изображения
      /popup
        popup.css            // Стили для компонента окна сохранения
    index.js                 // Точка входа микрофронтенда
  package.json               // Зависимости и скрипты микрофронтенда
  webpack.config.js
/host-microfrontend
  /src
    /components
      App.js                 // Компонент основной
      Footer.js              // Компонент футер
      Header.js              // Компонент хедер
      InfoTooltip.js         // Компонент информационное окно
      Main.js                // Компонент для отображения списка с карточками изображений
      PopupWithForm.js       // Компонент диалогового окна сохранения
      ProtectedRoute.js      // Компонент маршрутизатор
    /contexts
      CurrentUserContext.js  // Контекст
    /styles
      /footer
        footer.css           // Стили для компонента футера
      /header
        header.css           // Стили для компонента хедера
      /page
        page.css             // Стили для списка с карточками изображений
      /profile
        profile.css          // Стили для компонента профиля
    /utils
      api.js
    index.js                 // Точка входа микрофронтенда
  package.json               // Зависимости и скрипты микрофронтенда
  webpack.config.js

```

# Задание 2
Декомпозировать веб-приложения на `Django` на микросервисы в онлайн-редакторе `draw.io`.

*TODO-1: Разбить [исходную схему монолитного решения](https://code.s3.yandex.net/software-architecture/file/arch_template_task2.drawio?etag=11d456142d50853451c2e6001736c0a8) на сервисы, используя подход Domain-Driven Design.*

### ✅ Solution

Схема декомпозиции монолитного решения доступна по [ссылке](https://github.com/olpotkin/mesto-architecture-sprint-1/blob/mesto/sprint-1-task-2.drawio)
*(см. вкладку `Decomposition`)*
