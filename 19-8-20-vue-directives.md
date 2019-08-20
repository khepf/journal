### v-for
### v-if
### v-model
### v-bind
### v-on


#### Create Vue.js Directive
```
Vue.directive('purple', function (el) {
  el.style.color = 'purple'
})

new Vue({
  el: "#app",
  data: {}
})
```

```
<div id="app">
  <h1 v-purple>VueSchool</h1>
</div>
```

#### Custom Directive's Value
```
Vue.directive('switching-color', function (el, binding) {
  const colors = binding.value
  let i = 0
  setInterval(() => {
    el.style.color = colors[i++]
    if (i > colors.length - 1) {
      i = 0
    }
  }, 500)
})

new Vue({
  el: "#app",
  data: {}
})
```

```
<div id="app">
  <h1 v-switching-color="['purple', 'gold', 'pink', 'blue']">VueSchool</h1>
</div>
```

#### Directives are Reactive

```
Vue.directive('switching-color', function (el, binding) {
  const colors = binding.value
  let i = 0
  setInterval(() => {
    el.style.color = colors[i++]
    if (i > colors.length - 1) {
      i = 0
    }
  }, 500)
})

new Vue({
  el: "#app",
  data: {
    colors: ['purple', 'gold', 'pink', 'blue']
    },
  mounted () {
    this.colors.push("red")
   }
})
```
```
<div id="app">
  <h1 v-switching-color="colors">Hello There</h1>
</div>
```
