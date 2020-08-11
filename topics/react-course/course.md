```babel
babel src/app.js --out-file=public/scripts/app.js --presets=env,react --watch
```


```javascript
//Visibility Toggle
class VisibilityToggle extends React.Component {
    constructor(props) {
        super(props);
        this.handleVisibility = this.handleVisibility.bind(this);
        this.state = {
            visibility: false
        }
    }

    handleVisibility() {
        this.setState((prevState) => {
            return {
                visibility: !prevState.visibility
            }
        })
    }

    render() {
        return (
            <div>
                <h1>Visibility Toggle</h1>
                <button onClick={this.handleVisibility}>
                    {this.state.visibility ? 'Hide Content' : 'Show Content'}
                </button>
                {this.state.visibility && (
                    <div>
                        <p>It's gonna take a lot to drag me away from you</p>
                        <p>There's nothing that a hundred men or more could ever do</p>
                        <p>I bless the rains down in Africa</p>
                        <p>Gonna take some time to do the things we never had</p>
                    </div>
                )}
            </div>
        )
    }
}

ReactDOM.render(<VisibilityToggle />, document.getElementById('app'));
```


## ES6 import/export

```javascript
//utils.js
const square = x => Math.pow(x, 3);
const add = (a, b) => a + b;

export { square, add };

//app.js
import { square, add } from './utils'

console.log(square(10))
console.log(add(43, 26))
```

```javascript
// utils.js
export const square = x => Math.pow(x, 3);
export const add = (a, b) => a + b;

//You can directly export them as well
```

### Default Export

```javascript
//utils. js
const subtract = (a, b) => a - b;

export { square, add, subtract as default };

//app.js
//You have to add subtract before the curly braces because it is a default export
import subtract, { square, add } from './utils'
```

One can have only one default export per file. When we import we have to specify a name and import like:

```javascript
// import
import MyDefaultComponent from "./MyDefaultExport";
// export
const MyComponent = () => {}
export default MyComponent;
```


### Importing NPM Modules

There are 3 steps: install, import and use.

```bash
npm install validator
```
```javascript
import validator from 'validator'

console.log(validator.isEmail('test@gmail.com')) // returns true
```

```bash
yarn add react react-dom
```
```javascript
import React from 'react' // es6
import ReactDOM from 'react-dom'// es6
```

### Setting Up Babel with Webpack

```bash
yarn add babel-core babel-loader
```

```javascript
//webpack.config.js
module.exports = {
    entry: './src/app.js',
    output: {
        path: path.join(__dirname, 'public'),
        filename: 'bundle.js'
    },
    module: {
        rules:[{
            loader: 'babel-loader', 
            test: /\.js$/,
            exclude: /node_modules/
        }]
    }
};
```

Create new `.babelrc` file in the root folder of your app.

```javascript
//.babelrc
{
    "presets": [
        "env",
        "react"
    ]
}
```