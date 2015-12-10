Sails Isomorphic React Demo
----------

A simple demo app (a to-do list) demostrating isomorphic React served on Node.js and Sails.js.

<img src="https://github.com/desmat/sails-react-demo/blob/static/screenshot.png?raw=true"></img>


### Getting Started

```
git clone git@github.com:desmat/sails-react-demo.git
cd sails-react-demo
npm install
sails lift
```

### What is Isomorphic React?

Simply put, your React components will be rendered on the back-end AND front-end. The main benefit will be a more solid feel to the app from the user's perspective. Typical 'front-end oriented' web apps usually serve a very basic html page and let the javascript render the rest, resulting in flicker and often a perseved slow load time.

Instead this app will deliver a fully-rendered html document, often including fully rendered data-driven components, followed by typical React front-end stuff such as dynamic DOM manipulation.

Added benefits: simple urls, potentially cacheable server-side responses, better SEO support.


### How?

Basic isomorphism: 

* Create your React components normally
* Define your React Routes normally

<strong>At this point the static parts of your components will render on the back-end automatically.</strong> The next steps will allow you to fully render data-driven components isomorphically:

* Define restful api end-points corresponding to the component
```
sails generate model Foo
```
* Associate the route with the api end-point(s) via the attribute 'model'
```
<Route path="/foo" component={Foo} model="Foo"/>
	<Route path="/bar" component={Bar} model="Bar"/>
</Route>	
```
* Implement the component's getInitialState and componentDidMount by pulling data from Api.getInitial and Api.get respectively
```
...
getInitialState() {
	return {data: Api.getInitial('Foo')};
},  

componentDidMount() {
	Api.get('Foo', function(data) { 
		/* update front-end state */
	});
},
...

```

That's it!


### But HOW?!!

By leveraging React's renderToString method and the React router, plus a few hacks.

Painful details here:
* https://github.com/desmat/sails-react-demo/blob/master/components/utils/ServerSideRenderer.jsx
* https://github.com/desmat/sails-react-demo/blob/master/components/utils/ClientSideRenderer.jsx
* https://github.com/desmat/sails-react-demo/blob/master/assets/js/Api.js (get and getInitial methods)


### What's Next/Limitations

* Authentication
* More complex data end-point support
