# @maticonoffice/document-editor-react

[RU](README.md) | [EN](README.en.md)

Этот репозиторий содержит React-компонент для [Maticon Office Document Server](https://github.com/MaticonOffice/DocumentServer).

## Установка

Установите пакет из **npm** в свой проект:

```bash
npm install --save @maticonoffice/document-editor-react
```

или:

```bash
yarn add @maticonoffice/document-editor-react
```

## Использование

Пример использования компонента:

```jsx
...
import { DocumentEditor } from "@maticonoffice/document-editor-react";
...
...
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
...
...
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
    }
  }}
  events_onDocumentReady={onDocumentReady}
  onLoadComponentError={onLoadComponentError}
/>
...
```

## API

### Props

| Имя | Тип | По умолчанию | Обязательный | Описание |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| `id` | string | null | yes | Уникальный идентификатор компонента. |
| `documentServerUrl` | string | null | yes | Адрес Maticon Office Document Server. |
| `config` | object | null | yes | Общий объект конфигурации для открытия файла с токеном. [Config API](https://api.maticonoffice.ru/editors/config/) |
| `onLoadComponentError` | (errorCode: number, errorDescription: string) => void | null | no | Функция, вызываемая при ошибке загрузки компонента. |
| `document_fileType` | string | null | no | Тип файла. |
| `document_title` | string | null | no | Имя файла. |
| `documentType` | string | null | no | Тип документа. |
| `height` | string | null | no | Высота документа в окне браузера. |
| `type` | string | null | no | Тип платформы для доступа к документу: desktop, mobile или embedded. |
| `width` | string | null | no | Ширина документа в окне браузера. |
| `events_onAppReady` | (event: object) => void | null | no | Функция, вызываемая после загрузки приложения в браузере. |
| `events_onDocumentStateChange` | (event: object) => void | null | no | Функция, вызываемая при изменении документа. |
| `events_onMetaChange` | (event: object) => void | null | no | Функция, вызываемая при изменении метаинформации документа с помощью команды meta. |
| `events_onDocumentReady` | (event: object) => void | null | no | Функция, вызываемая после загрузки документа в редакторе. |
| `events_onInfo` | (event: object) => void | null | no | Функция, вызываемая после открытия файла приложением. |
| `events_onWarning` | (event: object) => void | null | no | Функция, вызываемая при предупреждении. |
| `events_onError` | (event: object) => void | null | no | Функция, вызываемая при ошибке или другом специальном событии. |
| `events_onRequestSharingSettings` | (event: object) => void | null | no | Функция, вызываемая при попытке управлять правами доступа к документу через кнопку _Change access rights_. |
| `events_onRequestRename` | (event: object) => void | null | no | Функция, вызываемая при попытке переименовать файл через кнопку _Rename..._. |
| `events_onMakeActionLink` | (event: object) => void | null | no | Функция, вызываемая при запросе ссылки для открытия документа с закладкой и переходом к ней. |
| `events_onRequestInsertImage` | (event: object) => void | null | no | Функция, вызываемая при попытке вставить изображение через кнопку _Image from Storage_. |
| `events_onRequestSaveAs` | (event: object) => void | null | no | Функция, вызываемая при попытке сохранить копию через кнопку _Save Copy as..._. |
| `events_onRequestMailMergeRecipients` | (event: object) => void | null | no | Функция, вызываемая при выборе получателей через кнопку _Mail merge_. |
| `events_onRequestCompareFile` | (event: object) => void | null | no | Функция, вызываемая при выборе документа для сравнения через кнопку _Document from Storage_. |
| `events_onRequestEditRights` | (event: object) => void | null | no | Функция, вызываемая при переходе из режима просмотра в режим редактирования через кнопку _Edit Document_. |
| `events_onRequestHistory` | (event: object) => void | null | no | Функция, вызываемая при запросе истории версий документа. |
| `events_onRequestHistoryClose` | (event: object) => void | null | no | Функция, вызываемая при возврате из истории версий к документу. |
| `events_onRequestHistoryData` | (event: object) => void | null | no | Функция, вызываемая при выборе определённой версии в истории документа. |
| `events_onRequestRestore` | (event: object) => void | null | no | Функция, вызываемая при восстановлении версии файла из истории. |

## Storybook

Измените адрес Document Server в файле *config/default.json*:

```json
"documentServerUrl": "http://documentserver/"
```

### Сборка Storybook

```bash
yarn build-storybook
```

### Запуск Storybook

```bash
yarn storybook
```

## Разработка

### Клонирование проекта из GitHub

```bash
git clone https://github.com/MaticonOffice/document-editor-react
```

### Установка зависимостей

```bash
yarn install
```

### Запуск тестов

```bash
yarn test
```

### Сборка проекта

```bash
yarn rollup
```

### Создание пакета

```bash
npm pack
```

## Обратная связь и поддержка

Если у вас возникли проблемы, вопросы или предложения по React-компоненту Maticon Office Document Server, обратитесь к разделу [Issues](https://github.com/MaticonOffice/document-editor-react/issues).

Официальный сайт проекта: [www.maticonoffice.ru](https://www.maticonoffice.ru/).

Форум поддержки: [forum.maticonoffice.ru](https://forum.maticonoffice.ru/).
