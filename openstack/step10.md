## Contract Testing - Provider Implementation

In a previous step, our Consumer utilised the Pact framework to generate consumer contracts called pact files, containing the interactions between the consumer, and this particular provider. Traditionally users of the Pact framework would leverage a Pact Broker as a central store for contracts, which consumers and providers can query to determine the status of integrations between applications, however when starting out, we advise that teams just share contracts manually whilst proving out the value for their teams.

In our case, we will leverage Pacts Provider verifier functionality, which will read in interactions from a pact file, and replay these against the Provider. The provider will issue its response to the Pact framework, which compares it against the consumers expectations. Errors and mis-matches are shown to the Provider team, and if using a Pact-Broker, can be reported back for collaboration and discussion between both consumer and provider teams.

Running the tests out the box, will result in a failure on two endpoints.

1. The first test shows a failure, due to the data returned in the Providers response. The shape on the response schema is correct, but the values are not those explicitly defined in the consumer contract. Pact provides a feature called Matchers, which allows for flexibility on the matching on the provider side.
   1. You can update the api.test.ts in the consumer codebase to have a `like` matcher wrapped around the expected `response` object in the Provider mock.
2. The second test shows a failure due to it requesting the product `id_example`. This product does not exist in our product repository.
   1. Pact provides a feature called Provider states which allows a consumer to define a particular state for the test data, prior to a verification being performed. We can update our state to `a product with ID 10 exists` and update our test to use the more realistic id `10` rather than `id_example`
   2. Alternatively, we could update our state to `a product with ID id_example exists` and then our provider would need to map that state, and create the `id_example`.
   3. You can see the provider states defined in `example-bi-directional-provider-soapui/src/product/pact.setup.js`. It is worth considering that provider states do introduce some cross-boundary dependency and synchronization. This is a suitable trade-off in our opinion as the benefits of doing so, allow the consumer/provider to exercise more scenarioes (a product exists, a product doesn't exist, a product returns an error), without a huge speed penalty versus integration tests, and without the inherit difficulty of creating different response types in integration environments where test data may not be as tightly controlled versus as a unit testing level.

### Tools Used

1. Pact

### Steps

1. Use Pact to replay the consumers contract expectations, against the provider implementation.
   1. `make docker_stop_all`{{exec}} - Stop our docker containers, as one of the ports conflicts with the below test
   2. `make provider_project_pact_verification`{{exec}}

### Check

Before moving to the next step, check the following:

1. You have stopped the Docker containers to avoid port conflicts
2. You have been able to run the Pact provider verification tests, and see the output of the test results in your console.