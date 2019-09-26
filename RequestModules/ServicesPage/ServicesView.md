1. Pick a File
  - ServicesView.vue
  
2. Find all the dispatches in there that fetch data.
  - dispatchEnvironmentServices
    - ```await dispatchEnvironmentServices(this.$store, this.environmentId);``` line 276
    - calls fetchEnvironmentServices action in services.ts
      - does a fetch to endpoint ```GET /api/cicada/environments/${environmentId}/serviceSummaries ```
      - operation ID = ```getServiceSummaries```
    - Note all getters and mutations
      - ```commitEnvironmentServices``` , a wrapper around the mutation ```SET_SELECTED_ENVIRONMENT_SERVICES```
      - state modified: ```state.selectedEnvironment.services```
        - The module state itself has the type ```IServicesState```, and that in that type the property ```selectedEnvironment``` has the type ```ISelectedEnvironment```
      - getters: ```getters.services``` that gets exported wrapper as ```getEnvironmentServices```

3. Replace each dispatch and associated data mutations and getters:
  - ```dispatchEnvironmentServices``` which hits ```GET /api/cicada/environments/${environmentId}/serviceSummaries ```
  3.1. Define a new Request Creator in the appropriate requests file in /src/util/requests/cicada/.
    - name: getServiceSummaries
    - parameters: environmentId: number, expandAll?: boolean, navigate?:string, serviceId?: number
    - response body: ```GetServiceSummariesResponse```
  3.2. Comment Out Or Delete The Old Stuff
  3.3. Update Code
  3.4. Clean Up
