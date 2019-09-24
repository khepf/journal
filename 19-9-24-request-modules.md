### 1. Pick a file
- ServicesPage/ServicesView.vue

### 2. Find all the dispatches in there that fetch data
- dispatch on line 276 ```await dispatchEnvironmentServices(this.$store, this.environmentId);```
which calls the action:
```
export const dispatchEnvironmentServices = dispatch(
  actions.fetchEnvironmentServices
);
``` 
from line 869 of services.ts

- This does a fetch to the endpoint GET /api/cicada/environments/${environmentId}/serviceSummaries (line 275)
- that endpoint has an operation ID of getServiceSummaries

- note associated getters and mutations to remove later:
  - commitEnvironmentServices (line 277), a wrapper around the mutation SET_SELECTED_ENVIRONMENT_SERVICES
  - what state is modified? state.selectedEnvironment.services
  - what getters touch state.selectedEnvironment.services? getters.services
    - this gets exported as the wrapper getter getEnvironmentServices

### 3. Replace each dispatch and associated data mutations and getters 
- dispatchEnvironmentServices which hits GET /api/cicada/environments/${environmentId}/serviceSummaries

#### 3.1 Define a new Request Creator in the appropriate requests file in /src/util/requests/cicada/
1. Find out where it's defined in swagger. It has a prefix of /environments
2. Define a new Request Creator in src/util/requests/cicada/environmentsRequests.ts
3. - Name: Operation ID is getServiceSummaries so that's what the name will be.
  - Parameters: look at swagger UI entry, this one has 1 required and 4 optional parameters
  - Response Body: 200 response in swagger is called getServiceSummariesResponse
#### Comment Out Old Stuff
1. the services property of ISelectedEnvironment interface
2. the initial state in the module definition at state.selectedEnvironment.services
3. The fetchEnvironmentServices and its exported wrapper
4. The mutation mutations.SET_SELECTED_ENVIRONMENT_SERVICES and its exported wrapper
5. The getter getters.services and its exported wrapper
