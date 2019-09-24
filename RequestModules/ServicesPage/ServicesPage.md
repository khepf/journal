1. Pick a file - ServicesPage/ServicesPage.vue

2. Find all the dispatches in there that fetch data.
  - 1 dispatch on line 87: dispatchEnvironmentDetails(store, environmentId)
    - This is a dispatch wrapper that calls the fetchEnvironmentDetails action in services.ts
      - This does a fetch to the endpoint GET ```/api/cicada/environments/${environmentId}/detail```
      - that endpoint has an operation ID of ```getEnvironmentDetail```
    - note all associated getters and mutations to remove later
      - a call to commitEnvironmentDetails, a wrapper around the mutation ```SET_SELECTED_ENVIRONMENT_DETAILS```
      - what state is modified? ```state.selectedEnvironment.details```
      - getters that touch ```state.selectedEnvironment.details```?
        - getters.environmentDetails. That gets exported as the wrapped getter named getEnvironmentDetails().
        
3. Replace each dispatch and associated data mutations and getters:
  - just that one mentioned above, dispatchEnvironmentDetails, which hits GET /api/cicada/environments/${environmentId}/detail.
  
3.1. Define a new Request Creator in the appropriate requests file in /src/util/requests/cicada/.
  1. Find the endpoint in Swagger
  2. Define a new Request Creator in the file src/util/requests/cicada/environmentsRequests.ts
  3. Request Creator has:
    - name: the method is GET, the operation ID is getEnvironmentDetail
      - so the name will be ```getEnvironmentDetail```
    - parameters:  Swagger UI entry has only 1 parameter, which is environment_id
      - converts to environmentId: number
    - response body
      - The 200 response interface is given as GetEnvironmentDetailResponse (found in model)
3.2 Create a seperate Interface called ```IGetEnvironmentDetailResponse``` inside the file ```/src/interfaces/requests/IGetEnvironmentDetailResponse.interface.ts```

3.3 Comment Out The Old Stuff
  - the details property of the ```ISelectedEnvironment``` interface
  - the initial state in the module definition at ```state.selectedEnvironment.details```
  - the action actions.fetchEnvironmentDetails in services.ts and its exported wrapper
  - the mutation mutations.SET_SELECTED_ENVIRONMENT_DETAILS and its exported wrapper commitEnvironmentDetails.
  - the getter getters.environmentDetails and its exported wrapper.
  
3.4 Update Code
  1. Note all the errors in console now
    - both the removed state and the removed mutation are referenced in the action editEnvironment().
```
export const services = {
  // ...
  actions: {
    // ...
    async editEnvironment(
      servicesContext: IServicesContext,
      payload: {
        componentId: number;
        env: IEnvironmentUpdatePayload;
      }
    ): Promise<any> {
      try {
        const res = await axios.put(
          `/api/cicada/components/${payload.componentId}/environments/${payload.env.id}`,
          payload.env
        );

        commitSetAlert(servicesContext as any, {
          state: true,
          style: 'success',
          msgs: res.data.messages || [
            { text: 'Successfully modified environment.' },
          ],
        });
        // // Update state with what has been edited
        // const details = servicesContext.state.selectedEnvironment.details;
        // details.url = payload.env.url;
        // commitEnvironmentDetails(servicesContext, details);
        const refreshRequest = getEnvironmentDetail({
          environmentId: payload.env.id,
        });
        await dispatchRequestIfNotNullAndCatch(
          servicesContext as ActionContext<any, IRootState>,
          refreshRequest
        );
        return true;
      } catch (err) {
        console.log('error', err);
        commitSetAlert(servicesContext as any, {
          state: true,
          style: 'error',
          msgs: [{ text: err }],
        });
        return false;
      }
    },
  },
};
```
3.5 Comment out unneeded imports
  - dispatchEnvironmentDetails
  - getEnvironmentDetails
3.6 We need to replace:
  - this.environmentDetails with a computed prop (a getter) that uses readRequestDataOrNotAsked().
  - To use that, we'll need a new computed prop (getter) that gives the request itself.
  - We'll then also replace the call to dispatchEnvironmentDetails() with dispatchRequestIfNotNullAndCatch().
  - Once we have that, we can replace this.isLoading with another computed prop that checks if the request data is AsyncData.Waiting.
  
3.7 Since we changed this.environmentDetails from some interface type to AsyncData<IGetEnvironmentDetailResponse, Error>, we'll need to update EnvironmentDetails.vue

3.8 Clean Up - Remove commented out code

  
      
