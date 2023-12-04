## Mocking

Prototype your API without writing any code.

<img width="979" alt="Screenshot 2023-12-04 at 17 16 59" src="https://github.com/SmartBear-DevRel/openstack/assets/19932401/a2f8481c-768d-4559-bf89-186d80438326">

[Prism](https://stoplight.io/open-source/prism) is an open-source HTTP mock server that can emulate your API's behavior as if you already built it. Mock HTTP servers are generated from your OpenAPI v2/v3 documents.

- Iterate faster with early feedback.
![iterate](https://assets-global.website-files.com/6320e912264435aca2ab0351/648bd673d9fa498a8b05caf9_prism-1-p-1080.webp)
  - Embrace the power of early feedback by incorporating user input during the design phase of your API, rather than waiting until after the code is written. This proactive approach significantly reduces the cost of change, allowing you to quickly iterate and refine your API based on real-world insights and requirements.

- Develop in parallel.
  - Maximize efficiency by enabling frontend and backend teams to work simultaneously. With Prism's mock server, frontend developers can start building against the API without waiting for the backend to be completed. This parallel development approach significantly accelerates API development and streamlines team collaboration.

- Generate dynamic examples.
![examples](https://assets-global.website-files.com/6320e912264435aca2ab0351/648bd7073f76e5ce364d13a5_prism-2.webp)
  - Static examples in mock APIs can bias the way you write the code and test the API. Prism generates dynamic, random examples based on your API description, ensuring validity and versatility.

- Validate input and output.
![validate](https://assets-global.website-files.com/6320e912264435aca2ab0351/648bd71baece84687093ccb0_prism-3.webp)
  - Prism validates both request and response data. If your specification contains an invalid example or your request isn't compliant with your API description, Prism can flag it for you, without yelling, we promise.

- Mocking callbacks.
![callbacks](https://assets-global.website-files.com/6320e912264435aca2ab0351/648bd72790d3b765fdb4f572_prism-4.webp)
  - Go beyond standard API interactions with Prism. OpenAPI v3.0 allows API designers to define callbacks and construct URLs for payload delivery. Prism supports this functionality, enabling you to integrate callbacks even before the API is built.

- Validation proxy.

  - Identify discrepancies between the OpenAPI document and target API to help frontend developers integrating with your API. Enable the proxy in pre-prod environments to ensure that OpenAPI documents and code stay in sync.

### Steps

We will run Stoplight Spectral locally with Docker, pulling the image from Dockerhub.

We will then mount a volume containing our OpenAPI description into the Docker container.

Finally we will tell Prism the location of our API file and tell it to start a `mock` which will be available on `http://localhost:3001` and will automatically have our API routes exposed alongside our test data.

You'll note some validation errors here, which align with those seen in Spectral, allowing you to ensure that the mocks you provide, are consistent with your codebase.

1. `make provider_mock_prism`{{exec}}
2. `curl localhost:3001/products`{{exec}} in terminal 2
3. Press `ctrl + c` to close the mock running in terminal 1

This mock provider can now be hosted, and linked up to your Swagger Editor / UI, allowing consumers to utilise the try-it-now functionality, where they can make requests from their browser.

### Check

Before moving to the next step, check the following:

1. You have been able to run `stoplight prism` locally serving a mock provider generated from our API description.
2. You have been able to make a HTTP request to `http://localhost:3001/products` resulting in a response from the mock provider
