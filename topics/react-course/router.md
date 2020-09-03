### Routing

Routing is the mechanism by which requests are connected to some code. It is essentially the way you navigate through a website or web-application. By clicking on a link, the URL changes which provides the user with some new data or a new webpage.

### Server-side

When browsing, the adjustment of a URL can make a lot of things happen. This will happen regularly by clicking on a link, which in turn will request a new page from the server. This is what we call a server-side route. A whole new document is served to the user.
A server-side request causes the whole page to refresh. This is because a new GET request is sent to the server which responds with a new document, completely discarding the old page altogether.

#### Pros: 

* A server-side route will only request the data that’s needed. No more, no less.

* Because server-side routing has been the standard for a long time, search engines are optimised for webpages that come from the server.

#### Cons

* Every request results in a full-page refresh. That means that unnecessary data is being requested. A header and a footer of a webpage often stays the same.

* It can take a while for the page to be rendered. However, this is only the case when the document to be rendered is very large or when you have slow internet speed.


### Client-side

A client-side route happens when the route is handled internally by the JavaScript that is loaded on the page. When a user clicks on a link, the URL changes but the request to the server is prevented. The adjustment to the URL will result in a changed state of the application. The changed state will ultimately result in a different view of the webpage. This could be the rendering of a new component, or even a request to a server for some data that the application will turn into some HTML elements.

It is important to note that the whole page won’t refresh when using client-side routing. There are just some elements inside the application that will change.

#### Pros

* Because less data is processed, routing between views is generally faster.

* Smooth transitions and animations between views are easier to implement.

#### Cons

* The whole website or web-application needs to be loaded on the first request. That’s why the initial loading time usually takes longer.

* Because the whole website or web-application is loaded initially, there is a possibility that there is data downloaded for views you won’t even come across.

* It requires more setup work or even a library. Because server-side is the standard, extra code must be written to make client-side routing possible.

* Search engine crawling is less optimised. Google is making good progress on crawling single-paged-apps, but it isn’t nearly as efficient as server-side routed websites.


## React Router

“React Router keeps your UI in sync with the URL. It has a simple API with powerful features like lazy code loading, dynamic route matching, and location transition handling built right in. Make the URL your first thought, not an after-thought.”

Install `npm install react-router-dom`

```javascript
import {
  BrowserRouter as Router,
  Switch,
  Route,
  Link
} from "react-router-dom";
```
For Example: 

```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import { BrowserRouter, Route } from 'react-router-dom';

const ExpenseDashboardPage = () => {
    return (
        <div>
            <p>This is the dashboard component</p>
        </div>
    )
}

const AddExpensePage = () => {
    return (
        <div>
            <p>This is the add-expense component</p>
        </div>
    )
}

const routes = (
    <BrowserRouter>
    <div>
        <Route path="/" component={ExpenseDashboardPage} />
        <Rout path="/create" component={AddExpensePage}>
    </div>
    </BrowserRouter>
);

ReactDOM.render(routes, document.getElementById('app'));
```