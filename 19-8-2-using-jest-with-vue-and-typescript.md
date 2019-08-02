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
- add "^.+\\.tsx?$": "ts-jest" to jest.transform in package.json
- add "testRegex": "(/\_\_tests\_\_/.*|(\\.|/)(test|spec))\\.(jsx?|tsx?)$" to jest field in package.json
- create \_\_tests\_\_ folder in src/components
- npm install @types/jest
- add "jest" to "types" in tsconfig.json
- add HelloWorld.spec.ts to project
```
// src/components/__tests__/HelloWorld.spec.ts
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

------
### Testing Vue with Jest
https://alligator.io/vuejs/testing-vue-with-jest/
