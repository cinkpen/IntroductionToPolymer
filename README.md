
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

This command serves the app at `http://127.0.0.1:8001/components/polymer-starter-kit/` and provides basic URL
routing for the app:

    polymer serve

---
### What's in this example

This application fetches data from the jsonplaceholder.typecode.com RESTful play area


index.html -> Loads the Main component with a couple of properties

```html
 <my-app api="https://jsonplaceholder.typicode.com" qty="10"></my-app>
```

my-app.html -> A Polymer component which houses the entire application
It has two properties an api address which is where the RESTful API lives, and a qty which is number of lines to show

```javascript
class MyApp extends Polymer.Element {
      static get is() { return 'my-app'; }

      static get properties() {
        return {
          api: String,
          qty: Number,
        }
      }

      ready() {
        super.ready();
      }
    }
```

search-test.html -> A Polymer component which asks the user to search for something, and raises custom events using Observables
```javascript
 var observable = Rx.Observable.fromEvent(this.$.input1, "keyup")
          .map(event => event.target.value)
          .debounce(this.debounce)
          .distinctUntilChanged();

        observable.subscribe(data => {
          console.log(data);
          this.dispatchEvent(new CustomEvent('changed', { detail: data }));
        });
```


service-1.html -> A polymer component - which has no template. This is used to encapsulate the call to the RESTful service
Note, how it uses RXjs to create a stream result.
Often it is useful to use Observables in the code - so that we can evolve into using more reactive web apps.
```javascript
 getData() {
                var observable = Rx.Observable.create(observer => {
                    var root = this.api;
                    var url = root + "/posts";

                    fetch(url).then(response => {
                        response.json()
                            .then(data => {
                                for (var i = 0, len = data.length; i < len; i++) {
                                    observer.next(data[i]);
                                }
                            });
                    })
                });
                return observable;
            }
```


component-1.html -> This brings together the UI Control, the service and how to bind arrays of data

```html
<template>
    <style>
      :host {
        display: block;
        padding: 10px;
      }
    </style>
    <div>
      <search-test on-changed="searchChanged"></search-test>
    </div>
    <ul>
      <template is="dom-repeat" items="[[data]]">
        <li>
          <user-1 data="[[item]]"></user-1>
        </li>
      </template>
    </ul>

    <service-1 id="service1" api="[[api]]"></service-1>
  </template>
```


### Additional Polymer resources

[![Polymer on Youtube](http://img.youtube.com/vi/HgJ0XCyBwzY/0.jpg)](https://www.youtube.com/watch?v=HgJ0XCyBwzY)

[Check out the Vaadin open source community code](https://github.com/vaadin/vaadin-grid)