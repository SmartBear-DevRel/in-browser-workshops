## Functional Testing - Provider Mock Implementation

Create functional tests for SoapUI, driven from the OpenAPI Specification.

Test these against our mock provider (provided by Prism), in order to verify the test suite / mock implementation, and prepare for verifying our provider codebase once implemented.

### Tools Used

1. SoapUI
   1. OpenApi2SoapUI
2. Stoplight Prism

### Steps

We will first leverage another open-source project [OpenAPI2SoapUI](https://github.com/apiaddicts/openapi2soapui) built by the [ApiAddicts](https://github.com/apiaddicts) team.

This will allow us to quickly bootstrap a SoapUI project, from our API description in the OpenAPI format, generating the requests for each resource operation and a test suite. This test suite won't contain assertions, we can add these later, but it will give us some cursory coverage of a provider implementation.

We will utilise SoapUI using it's test runner, which is available on [DockerHub](https://hub.docker.com/r/smartbear/soapuios-testrunner).

We will leverage Prism to serve as our provider mock, as it hasn't yet been developed yet, it will be available on `http://localhost:3001`.

We will load in our project file, generated with `openapi2soapui`, into the soapui test runner, and tell the runner which endpoint our provider will be running on.

The tests will run, and should report 0 failures. You can stop the provider mock, and run the tests again. You should see three errors.

1. SoapUI
   1. 👉🏼 `make openapi2soapui_fetch`{{exec}}
   2. 👉🏼 `make openapi2soapui_build`{{exec}}
   3. 👉🏼 `make openapi2soapui_generate_project`{{exec}}
   4. 👉🏼 `make provider_mock_prism`{{exec}} - Run our Mock Provider
   5. In a second terminal 👉🏼 `make soapui_run`{{exec}} in terminal 2
      1. Don't forget to change directory into the 👉🏼 `cd openstack`{{exec}} beforehand in the new terminal
   6. Press 👉🏼 `ctrl + c` to close the mock running in terminal 1

### Check

Before moving to the next step, check the following:

1. You have been able to generate a SoapUI project from an OpenAPI description using `openapi2soapui`
2. You have been able to execute the SoapUI functional tests with it's test runner, against the provider mock.
