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