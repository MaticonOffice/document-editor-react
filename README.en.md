# @maticonoffice/document-editor-react

[RU](README.md) | [EN](README.en.md)

This repository contains the Maticon Office Docs React component, which integrates [Maticon Office Document Server](https://github.com/MaticonOffice/DocumentServer) into [React](https://react.dev/) projects.

**Please note:** Before working with this component, you need to install Maticon Office Docs. You can use [Docker](https://github.com/MaticonOffice/Docker-DocumentServer) for this purpose (recommended).

## Prerequisites

This procedure requires [Node.js and npm](https://nodejs.org/en).

## Creating the demo React application with Maticon Office Docs editor

This procedure creates a [basic React application](https://github.com/facebook/create-react-app) and installs a Maticon Office Docs editor in it.

1. Create a new React project named *maticonoffice-react-demo* using the *Create React App* package:
```bash
npx create-react-app maticonoffice-react-demo
```

2. Go to the newly created directory:
```bash
cd maticonoffice-react-demo
```

3. Install the Maticon Office Docs React component from **npm** and save it to the *package.json* file with *--save*:
```bash
npm install --save @maticonoffice/document-editor-react
```

4. Open the *./src/App.js* file in the *maticonoffice-react-demo* project and replace its contents with the following code:

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

Replace the following lines with your own data:
* **"http://documentserver/"** - replace it with your server URL;
* **"https://example.com/url-to-example-document.docx"** - replace it with your file URL;
* **"https://example.com/url-to-callback.ashx"** - replace it with your callback URL, which is required for saving.

This JavaScript file creates the *App* component containing the Maticon Office Docs editor configured with basic features.

5. Test the application using the Node.js development server:
* To start the development server, go to the *maticonoffice-react-demo* directory and run:
```bash
npm run start
```
* To stop the development server, select the command line or terminal and press *Ctrl+C*.

## Deploying the demo React application

The easiest way to deploy the application to a production environment is to install [serve](https://github.com/vercel/serve) and create a static server:

1. Install the *serve* package globally:
```bash
npm install -g serve
```

2. Serve your static site on port 3000:
```bash
serve -s build
```
You can specify another port with the *-l* or *--listen* flags:
```bash
serve -s build -l 4000
```

3. To serve the project folder, go to it and run the *serve* command:
```bash
cd maticonoffice-react-demo
serve
```

You can now deploy the application to the created server:

1. Go to the *maticonoffice-react-demo* directory and run:
```bash
npm run build
```
The *build* directory will be created with a production build of your application.

2. Copy the contents of *maticonoffice-react-demo/build* to the web server root directory (the *maticonoffice-react-demo* folder).

The application will be deployed on the web server (*http://localhost:3000* by default).

## API

### Props

| Name | Type | Default | Required | Description |
| ------------- | ------------- | ------------- | ------------- | ------------- |
| `id` | string | null | yes | Component unique identifier. |
| `documentServerUrl` | string | null | yes | Address of Maticon Office Document Server. |
| `shardkey` | string \| boolean | true | no | The string or boolean parameter required for load balancing during collaborative editing: all users editing the same document are served by the same server. [Shard key](https://api.maticonoffice.ru/docs/docs-api/get-started/how-it-works/#shard-key) |
| `config` | object | null | yes | Generic configuration object for opening a file with a token. [Config API](https://api.maticonoffice.ru/docs/docs-api/usage-api/config/) |
| `onLoadComponentError` | (errorCode: number, errorDescription: string) => void | null | no | Function called when an error occurs while loading the component. |

## Storybook

Change the Document Server address in *config/default.json*:
```json
"documentServerUrl": "http://documentserver/"
```

### Build Storybook
```bash
npm run build-storybook
```

### Start Storybook
```bash
npm run storybook
```

## Development

### Clone the project from GitHub
```bash
git clone https://github.com/MaticonOffice/document-editor-react
```

### Install project dependencies
```bash
npm install
```

### Run component tests
```bash
npm run test
```

### Build the project
```bash
npm run rollup
```

### Create the package
```bash
npm pack
```

## Feedback and support

If you have issues, questions, or suggestions about the Maticon Office Document Server React component, use the [Issues](https://github.com/MaticonOffice/document-editor-react/issues) section.

Official project website: [www.maticonoffice.ru](https://www.maticonoffice.ru/).

Support forum: [forum.maticonoffice.ru](https://forum.maticonoffice.ru/).
