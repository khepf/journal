### Using jest with typescript
https://vue-test-utils.vuejs.org/guides/using-with-typescript.html
- vue create hello-world
- manually create "choose typescript"
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
- add "testRegex": "(/__tests__/.*|(\\.|/)(test|spec))\\.(jsx?|tsx?)$" to jest field in package.json
- create __tests__ folder in src/components
- npm install @types/jest
- add "jest" to "types" in tsconfig.json

### Testing Vue with Jest
https://alligator.io/vuejs/testing-vue-with-jest/
