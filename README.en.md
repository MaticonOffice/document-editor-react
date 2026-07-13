# @maticonoffice/document-editor-react

[RU](README.md) | [EN](README.en.md)

This repository contains the React component for [Maticon Office Document Server](https://github.com/MaticonOffice/DocumentServer).

## Installation

Install it from **npm** in your project:

```bash
npm install --save @maticonoffice/document-editor-react
```

or:

```bash
yarn add @maticonoffice/document-editor-react
```

## Usage

The following example shows how to use the component:

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

| Name | Type | Default | Required | Description |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| `id` | string | null | yes | Component unique identifier. |
| `documentServerUrl` | string | null | yes | Address of Maticon Office Document Server. |
| `config` | object | null | yes | Generic configuration object for opening a file with a token. [Config API](https://api.maticonoffice.ru/editors/config/) |
| `onLoadComponentError` | (errorCode: number, errorDescription: string) => void | null | no | Function called when an error occurs while loading the component. |
| `document_fileType` | string | null | no | The file type. |
| `document_title` | string | null | no | The file name. |
| `documentType` | string | null | no | The document type. |
| `height` | string | null | no | Defines the document height in the browser window. |
| `type` | string | null | no | Defines the platform type used to access the document: desktop, mobile, or embedded. |
| `width` | string | null | no | Defines the document width in the browser window. |
| `events_onAppReady` | (event: object) => void | null | no | Function called when the application is loaded into the browser. |
| `events_onDocumentStateChange` | (event: object) => void | null | no | Function called when the document is modified. |
| `events_onMetaChange` | (event: object) => void | null | no | Function called when document metadata is changed with the meta command. |
| `events_onDocumentReady` | (event: object) => void | null | no | Function called when the document is loaded into the document editor. |
| `events_onInfo` | (event: object) => void | null | no | Function called when the application opens the file. |
| `events_onWarning` | (event: object) => void | null | no | Function called when a warning occurs. |
| `events_onError` | (event: object) => void | null | no | Function called when an error or another special event occurs. |
| `events_onRequestSharingSettings` | (event: object) => void | null | no | Function called when a user tries to manage document access rights with the _Change access rights_ button. |
| `events_onRequestRename` | (event: object) => void | null | no | Function called when a user tries to rename the file with the _Rename..._ button. |
| `events_onMakeActionLink` | (event: object) => void | null | no | Function called when a user requests a link that opens the document at a bookmark. |
| `events_onRequestInsertImage` | (event: object) => void | null | no | Function called when a user tries to insert an image with the _Image from Storage_ button. |
| `events_onRequestSaveAs` | (event: object) => void | null | no | Function called when a user tries to save a copy with the _Save Copy as..._ button. |
| `events_onRequestMailMergeRecipients` | (event: object) => void | null | no | Function called when a user selects recipients with the _Mail merge_ button. |
| `events_onRequestCompareFile` | (event: object) => void | null | no | Function called when a user selects a document for comparison with the _Document from Storage_ button. |
| `events_onRequestEditRights` | (event: object) => void | null | no | Function called when a user switches from viewing to editing with the _Edit Document_ button. |
| `events_onRequestHistory` | (event: object) => void | null | no | Function called when a user requests the document version history. |
| `events_onRequestHistoryClose` | (event: object) => void | null | no | Function called when a user returns to the document from version history. |
| `events_onRequestHistoryData` | (event: object) => void | null | no | Function called when a user selects a specific document version in history. |
| `events_onRequestRestore` | (event: object) => void | null | no | Function called when a user restores a file version from history. |

## Storybook

Change the Document Server address in *config/default.json*:

```json
"documentServerUrl": "http://documentserver/"
```

### Build Storybook

```bash
yarn build-storybook
```

### Start Storybook

```bash
yarn storybook
```

## Development

### Clone the project from GitHub

```bash
git clone https://github.com/MaticonOffice/document-editor-react
```

### Install project dependencies

```bash
yarn install
```

### Run component tests

```bash
yarn test
```

### Build the project

```bash
yarn rollup
```

### Create the package

```bash
npm pack
```

## Feedback and support

If you have issues, questions, or suggestions about the Maticon Office Document Server React component, use the [Issues](https://github.com/MaticonOffice/document-editor-react/issues) section.

Official project website: [www.maticonoffice.ru](https://www.maticonoffice.ru/).

Support forum: [forum.maticonoffice.ru](https://forum.maticonoffice.ru/).
