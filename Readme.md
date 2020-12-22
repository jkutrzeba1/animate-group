## animate-group

Use [animate.css](https://animate.style/) transitions to animate  *entry* and *leave* on list of items based on an array with smooth move of surrounding elements.

## Install
```bash
npm install animate-group --save
```
#### Import
```js
const AnimateGroup = require('animate-group').default;
```

#### Local registration
```js
  module.exports = {
    components: {
      AnimateGroup
    } ...
```

#### Global registration
```js
Vue.component('AnimateGroup', AnimateGroup);
```
## API
### Props

| Prop              | Type    | Description                                                                                                                                                                                                                          | Required | Default             |
|-------------------|---------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|---------------------|
| animationIn       | String  | Animation entry name                                                                                                                                                                                                                 | Y        |                     |
| animationOut      | String  | Animation leave name                                                                                                                                                                                                                 | Y        |                     |
| animationDuration |  Number | Animation duration in seconds                                                                                                                                                                                                        |          | Animate.css default |
| smoothMove        | Boolean | Specifies whether surrounding elements will occupy placement of inserted/removed element in smoothly way                                                                                                                             |          | true                |
| instantMove       | Boolean | Instant move of surrounding elements on leave transition - removed element will be detached from normal document flow.  Surrounding elements will be moved immediately - rather when animation ends. Applied only for out transition |          | true                |


### Slots


| Name      | Description                                              |
|-----------|----------------------------------------------------------|
| (default) | List of items based on array in form of v-for directive  |
