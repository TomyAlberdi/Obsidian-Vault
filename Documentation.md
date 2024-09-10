#Theory 
Properly documenting an API allows developers (whether internal or external to our team) to have an accessible approach to learning about our API/service. A well-structured documentation simplifies the process of understanding our API service and is one of the key components that shape a developer's experience when using our API services.
Just like assembly instructions for furniture, it must meet certain requirements that distinguish good documentation from indecipherable pages in unfamiliar languages. It goes beyond API response formats or [[authentication]] methods. The documentation should be interactive, showing developers the structure and organization that will make their work easier. This way, they won't have to spend time researching functions or waste it on completely unproductive tests.
## Documentation Tools
Developing an API requires a lot of effort. We must dedicate time to design and implementation, as well as to documentation and its maintenance, to ensure that developers who use it clearly understand how it works.
For this reason, there are API documentation tools that can make the task easier. The most well-known are RAML (RESTful API Modeling Language), Slate, and Swagger. The latter is one of the most widely used standards and was chosen by the Open API Initiative as the model for API specifications.
## Best Practices
### Detailed Endpoint Descriptions:
Expand the description of endpoints with the most detailed explanatory text possible, using understandable language. Avoid focusing too much on technical aspects, as not everyone has the same experience or familiarity with our API environment.
Although APIs serve as an abstraction layer to hide certain operational details, the best way to avoid confusing developers is precisely by minimizing abstractions in the documentation.
### Detailing [[Parameters]] and Expected Responses:
List all input and output parameters provided by each endpoint, along with the expected HTTP response types. This will prevent surprises for developers using the API and account for the various scenarios they must consider when developing an appropriate frontend.