# Javascript

## Testing - Jasmine
Keep your modules small
Always throw / return errors when you need to and check for them in your tests
- success, error, expected and unexpected data
Describe block - module
it block - function
  - passing the done param forces jasmine to assume it is an async function

mocks
- sinon, rewire, node-tap, require-inject
- should only be used when the final result is to call an external service ie db / external api
- used to verify a call against an external service

spies

doubles

Code coverage
- istanbul
