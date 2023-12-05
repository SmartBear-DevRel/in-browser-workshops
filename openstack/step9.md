## Functional Testing - Provider Implementation

In the previous step, we generated a client SDK using the Swagger Codegen project. Whilst it can also be used to generated a Provider implementation, it may be the case that you the Provider team have built their own codebase. In this example we will utilise a pre-built provider codebase, and run our SoapUI functional test suite, previously created and executed against our Provider mock supplied by Prism, it is now time to try it out against the real thing.

We will first start out provider codebase manually, and make some requests with our favourite HTTP client from the command line. We can see that the data returned differs from those in our mock, which was driven by the example data in our OpenAPI document.

We can then run our SoapUI tests, which will issue our requests for this provider implementation. For convenience, in continuous integration, a command is provided that will start our provider, then run our SoapUI tests, finally shutting down the server at the end.

### Tools Used

1. SoapUI

### Steps

1. Download a pre-prepared Provider implementation and try it out
   1. 👉🏼 `make provider_project_fetch`{{exec}}
   2. 👉🏼 `make provider_project_install`{{exec}}
   3. 👉🏼 `make provider_project_run`{{exec}} in terminal 1
   4. 👉🏼 `curl localhost:3001/products`{{exec}} in terminal 2
2. With the provider still running, run our SoapUI tests
   1. 👉🏼 `make provider_project_run`{{exec}} in terminal 1
   2. 👉🏼 `make soapui_run`{{exec}} in terminal 2
      1. Don't forget to change directory into the 👉🏼 `cd openstack`{{exec}} beforehand in the new terminal
   3. Press 👉🏼 `ctrl + c` to close the server running in terminal 1
3. Start the server and test, all in one, omitting the need for two terminals
   1. 👉🏼 `make provider_start_test_stop`{{exec}}

### Check

Before moving to the next step, check the following:

1. You have been able to run the provider implementation locally
2. You have been able to run the SoapUI project, against the provider implementation