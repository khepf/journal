### Unit Tests with Vuetify


### Using jest with typescript
https://vue-test-utils.vuejs.org/guides/using-with-typescript.html
- vue create hello-world
- manually create 
  - choose typescript, deselect all others
  - default choices for all others except 'Where do you prefer placing config for Babel, PostCSS, ESLint, etc.?' 
  - Choose 'In package.json'
  
- npm install --save-dev jest @vue/test-utils
- add "test:unit": "jest" to scripts in package.json
- npm install --save-dev vue-jest
- create a jest block in package.json
```
  "jest": {
    "moduleFileExtensions": [
      "js",
      "ts",
      "json",
      // tell Jest to handle `*.vue` files
      "vue"
    ],
    "transform": {
      // process `*.vue` files with `vue-jest`
      ".*\\.(vue)$": "vue-jest"
    },
    "testURL": "http://localhost/"
  }
```
- npm install --save-dev ts-jest
- add ``` "^.+\\.tsx?$": "ts-jest" ``` to jest.transform in package.json
- add ``` "testRegex": "(/__tests__/.*|(\\.|/)(test|spec))\\.(jsx?|tsx?)$" ``` to jest field in package.json
- create \_\_tests\_\_ folder in src/components
- npm install @types/jest
- add "jest" to "types" in tsconfig.json
- add HelloWorld.spec.ts to project
```
// src/components/__tests__/HelloWorld.spec.ts
import 'jest'
import { shallowMount } from '@vue/test-utils'
import HelloWorld from '../HelloWorld.vue'

describe('HelloWorld.vue', () => {
  test('renders props.msg when passed', () => {
    const msg = 'new message'
    const wrapper = shallowMount(HelloWorld, {
      propsData: { msg }
    })
    expect(wrapper.text()).toMatch(msg)
  })
})
```
- npm install babel-core babel-loader --save-dev
- npm run test:unit

------
### Testing Vue with Jest
https://alligator.io/vuejs/testing-vue-with-jest/

### TypeScript - Vue Starter
https://github.com/Microsoft/TypeScript-Vue-Starter

### TypeScript - Vue Todo App
https://github.com/DanielRosenwasser/typescript-vue-todomvc

### Unit test benefits
- Check components work correctly
- Provide documentation
- Easier debugging
- Less bugs

### Use compilation process (Compilers) as part of unit tests
- Webpack (vue-loader)
- Jest (vue-jest)
#### Component contract
- "If you provide me with this *input*, then I will generate this *output*"
##### Input
- User Action
- Props
- Store
##### Output
- Rendered output
- Vue events
- Function calls

```
<modal-component
  :visible="displayModal"
  :onClose="closeModal"
>
  Some Content
</modal-component>
```
```
<template>
  <div v-if="visible" class="modal is-active">
    <div class="modal-background"></div>
    <div class="modal-content">
      <div class="box">
        <button 
          @click="onClose"
          class="delete"
          aria-label="close"></button>
        <slot />
       </div>
      </div>
     </div>
  </div>
</template>

<script>
export default {
  props: ['visible', 'onClose']
}
</script>
```

```
test('does not render whan passed visible prop', () => {
  const wrapper = mount(Modal)
  expect(wrapper.isEmpty()).toBe(true)
})

test('renders when passed visible prop as true', () => {
  const wrapper = mount(Modal, {
    propsData: {
      visible: true
    }
   })
   expect(wrapper.isEmpty()).toBe(false)
})

test('calls onClose when button is clicked', () => {
  const onClose = jest.fn()
  const wrapper = mount(Modal, {
    propsData: {
      visible: true,
      onClose
    }
  })
  wrapper.find('button').trigger('click')
  expect(onClose).toHaveBeenCalled()
})
```
### Snapshot tests
```
test('renders correctly', () => {
  const wrapper = mount(Modal, {
    propsData: {
      visible: true
    }
  })
  expect(wrapper.html()).toMatchSnapshot()
})
```
- Snapshot checks if previos snapshot exists
  - if so, it compares snapshot to previous snapshot
  - if not, it creates a snashot and the test passes
``` 
npm install --save-dev jest-serializer-vue 
``` 
- formats snapshot output
```
"jest": {
  "snapshotSerializers": [
    "jest-serializer-vue"
   ],
 }
 ```
#### Overwrite snapshot
``` npm run unit -- -u ```

```
test('renders correctly', () => {
  const wrapper = mount(Modal, {
    slots: {
      default: '<p>some content</p>'
    },
    propsData: {
      visible: true
    }
  })
  expect(wrapper.html()).toMatchSnapshot()
})
```

### unit testing vs e2e testing
https://vuejsdevelopers.com/2019/04/01/vue-testing-unit-vs-e2e/


### UNIT TESTS

```
class User {
  constructor(details) {
    const { firstname, lastname } = details
    this.firstname = firstname
    this.lastname = lastname
  }
  get name() {
    return `${this.firstname} ${this.lastname}`
  }
 }
 ```
 ```
 describe('User', () => {
  test('name returns full name', () => {
    const user = new User({ firstname: 'Jane', lastname: 'Doe' })
    expect(user.name).toBe('Jane Doe')
    })
  })
```
- toEqual - to check complex comparisons like arrays and objects
##### beforeEach
```
import movies from './movies'

describe('Favorite Movies', () => {
  let myMovies = []
  beforeEach(() => {
    const myMovies = [{
      title: 'Age of Ultron',
      rate: null
    }]
  })
  
  test('can add a movie', () => {
    movies.add(myMovies, 'Avatar')
    expect(myMovies).toMatchSnapshot()
  })
   
  test('rate a movie', () => {
    movies.rate(myMovies[0], 5)
    expect(myMovies).toMatchSnapshot()
  })
 })
```
- test.only to run only that test
- test.skip to skip that particular test

```
// model.js
export default class Model {
  constructor() {
    this.$collection = []  
  }
  record() {}
  all() {}
  find() {}
  update() {}
}
```

```
// model.spec.js
import Model from './model'

test('new works', () => {
  expect(new Model).toBeInstanceOf(Model)
})

test('model structure', () => {
  expect(new Model).toEqual(expect.objectContaining({
    $collection: expect.any(Array),
    record: expect.any(Function),
    all: expect.any(Function),
    find: expect.any(Function),
    update: expect.any(Function),
  }))
})
```
