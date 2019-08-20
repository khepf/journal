### v-for
### v-if
### v-model
### v-bind
### v-on

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
