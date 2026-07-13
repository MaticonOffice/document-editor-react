# @maticonoffice/document-editor-react

[RU](README.md) | [EN](README.en.md)

Этот репозиторий содержит React-компонент Maticon Office Docs, который интегрирует [Maticon Office Document Server](https://github.com/MaticonOffice/DocumentServer) в проекты на [React](https://react.dev/).

**Обратите внимание:** перед работой с этим компонентом нужно установить Maticon Office Docs. Для этого можно использовать [Docker](https://github.com/MaticonOffice/Docker-DocumentServer) (рекомендуется).

## Предварительные требования

Для этой процедуры требуются [Node.js и npm](https://nodejs.org/en).

## Создание демонстрационного React-приложения с редактором Maticon Office Docs

Эта процедура создаёт [базовое React-приложение](https://github.com/facebook/create-react-app) и устанавливает в него редактор Maticon Office Docs.

1. Создайте новый React-проект с именем *maticonoffice-react-demo* с помощью пакета *Create React App*:
```bash
npx create-react-app maticonoffice-react-demo
```

2. Перейдите в созданный каталог:
```bash
cd maticonoffice-react-demo
```

3. Установите React-компонент Maticon Office Docs из **npm** и сохраните его в файле *package.json* с параметром *--save*:
```bash
npm install --save @maticonoffice/document-editor-react
```

4. Откройте файл *./src/App.js* в проекте *maticonoffice-react-demo* и замените его содержимое следующим кодом:

```jsx
import React, { useRef } from 'react';
import { DocumentEditor } from "@maticonoffice/document-editor-react";

var onDocumentReady = function (event) {
    console.log("Document is loaded");
};

var onLoadComponentError = function (errorCode, errorDescription) {
    switch(errorCode) {
        case -1: // Unknown error loading component
            console.log(errorDescription);
            break;

        case -2: // Error load DocsAPI from http://documentserver/
            console.log(errorDescription);
            break;

        case -3: // DocsAPI is not defined
            console.log(errorDescription);
            break;
    }
};

export default function App() {
    return (
        <>
            <DocumentEditor
                id="docxEditor"
                documentServerUrl="http://documentserver/"
                config={{
                    "document": {
                        "fileType": "docx",
                        "key": "Khirz6zTPdfd7",
                        "title": "Example Document Title.docx",
                        "url": "https://example.com/url-to-example-document.docx"
                    },
                    "documentType": "word",
                    "editorConfig": {
                        "callbackUrl": "https://example.com/url-to-callback.ashx"
                    },
                    "events": {
                        "onDocumentReady": onDocumentReady
                    }
                }}
                onLoadComponentError={onLoadComponentError}
            />
        </>
    );
}
```

Замените следующие строки своими данными:
* **"http://documentserver/"** — URL вашего сервера;
* **"https://example.com/url-to-example-document.docx"** — URL вашего файла;
* **"https://example.com/url-to-callback.ashx"** — URL callback-обработчика, необходимого для сохранения.

Этот JavaScript-файл создаст компонент *App*, содержащий редактор Maticon Office Docs с базовой конфигурацией.

5. Проверьте приложение с помощью development-сервера Node.js:
* Чтобы запустить development-сервер, перейдите в каталог *maticonoffice-react-demo* и выполните:
```bash
npm run start
```
* Чтобы остановить development-сервер, выберите командную строку или терминал и нажмите *Ctrl+C*.

## Развёртывание демонстрационного React-приложения

Самый простой способ развернуть приложение в production-окружении — установить [serve](https://github.com/vercel/serve) и создать статический сервер:

1. Установите пакет *serve* глобально:
```bash
npm install -g serve
```

2. Запустите статический сайт на порту 3000:
```bash
serve -s build
```
Другой порт можно указать с помощью флагов *-l* или *--listen*:
```bash
serve -s build -l 4000
```

3. Чтобы обслуживать папку проекта, перейдите в неё и выполните команду *serve*:
```bash
cd maticonoffice-react-demo
serve
```

Теперь приложение можно развернуть на созданном сервере:

1. Перейдите в каталог *maticonoffice-react-demo* и выполните:
```bash
npm run build
```
Будет создан каталог *build* с production-сборкой приложения.

2. Скопируйте содержимое каталога *maticonoffice-react-demo/build* в корневой каталог веб-сервера (в папку *maticonoffice-react-demo*).

Приложение будет развёрнуто на веб-сервере (*http://localhost:3000* по умолчанию).

## API

### Props

| Имя | Тип | По умолчанию | Обязательный | Описание |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| `id` | string | null | yes | Уникальный идентификатор компонента. |
| `documentServerUrl` | string | null | yes | Адрес Maticon Office Document Server. |
| `shardkey` | string \| boolean | true | no | Строковый или логический параметр для балансировки нагрузки при совместном редактировании: все пользователи, редактирующие один документ, обслуживаются одним сервером. [Shard key](https://api.maticonoffice.ru/docs/docs-api/get-started/how-it-works/#shard-key) |
| `config` | object | null | yes | Общий объект конфигурации для открытия файла с токеном. [Config API](https://api.maticonoffice.ru/docs/docs-api/usage-api/config/) |
| `onLoadComponentError` | (errorCode: number, errorDescription: string) => void | null | no | Функция, вызываемая при ошибке загрузки компонента. |

## Storybook

Измените адрес Document Server в файле *config/default.json*:
```json
"documentServerUrl": "http://documentserver/"
```

### Сборка Storybook
```bash
npm run build-storybook
```

### Запуск Storybook
```bash
npm run storybook
```

## Разработка

### Клонирование проекта из GitHub
```bash
git clone https://github.com/MaticonOffice/document-editor-react
```

### Установка зависимостей
```bash
npm install
```

### Запуск тестов
```bash
npm run test
```

### Сборка проекта
```bash
npm run rollup
```

### Создание пакета
```bash
npm pack
```

## Обратная связь и поддержка

Если у вас возникли проблемы, вопросы или предложения по React-компоненту Maticon Office Document Server, обратитесь к разделу [Issues](https://github.com/MaticonOffice/document-editor-react/issues).

Официальный сайт проекта: [www.maticonoffice.ru](https://www.maticonoffice.ru/).

Форум поддержки: [forum.maticonoffice.ru](https://forum.maticonoffice.ru/).
