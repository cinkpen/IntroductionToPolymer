
### Setup

##### Prerequisites

First, install [Polymer CLI](https://github.com/Polymer/polymer-cli) using
[npm](https://www.npmjs.com) (we assume you have pre-installed [node.js](https://nodejs.org)).

    npm install -g polymer-cli

Second, install [Bower](https://bower.io/) using [npm](https://www.npmjs.com)

    npm install -g bower


### Clone this repository

git clone https://github.com/cinkpen/IntroductionToPolymer

### Run bower 

bower install

### Start the development server

This command serves the app at `http://127.0.0.1:8081` and provides basic URL
routing for the app:

    polymer serve


### What's in this example

index.html -> Loads the Main component with a couple of properties

```
 <my-app api="https://jsonplaceholder.typicode.com" qty="10"></my-app>
```

