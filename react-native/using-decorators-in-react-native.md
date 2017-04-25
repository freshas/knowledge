# Using decorators in React-Native

## 1. Install the necessary transform utility

```sh
npm install --save babel-plugin-transform-decorators-legacy
# OR
yarn add babel-plugin-transform-decorators-legacy
```

## 2. Add the babel transform plugin to your `.babelrc`

```json
{
  "presets": ["react-native-stage-0"],
  "plugins": [
    "transform-decorators-legacy"
  ]
}
```

## 3. Use decorators

```js
@connect(mapStateToProps, mapActionsToProps)
export default class DecoratedComponent extends Component {
  componentDidMount() {
    this.props.loadSomething();
  }

  // ...
```
