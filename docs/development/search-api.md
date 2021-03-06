# Search API

## Documentation

OpenAPI Specification, Swagger documentation is generated by [SwashBuckle](https://github.com/domaindrivendev/Swashbuckle.AspNetCore).

The json is available at: `{base_url}/swagger/searchAPIdocs/swagger.json`, and the UI is available at: `{base_url}/swagger`

For local development on port 5000, that is [Here.](http://localhost:5000/swagger)

## Data Source

The search API communicates with the Enterprise Service Bus (ESB) which is hosted and maintained by the state of Alaska.
The documentation for the methods that the ESB provides are located [Here](https://esbtest.dhss.alaska.gov/swagger/)

The ESB is communicating with three separate systems to get the data it needs.
More information about those systems can be found in the [Data Sources Documentation](../getting-started/data-sources.md)

## Controllers

### Search

This controller is responsible for performing searches. It primarily searches the MCI system, which returns a list of users and their user IDs in ARIES and EIS.
Those IDs can then be used to get additional information from the respective system.

Method(s) for getting data:

- GetMci - This method takes three optional parameters: firstName, lastName, and registration (SSN). It will return a list of users which match the passed in criteria.

### Person

This contoller is responsible for getting data needed by the person details page. 

Method(s) for getting data:

- GetEisCases - This method requires a clientId parameter, and will return data from EIS for that user's cases
- GetAriesCases - This method requires a clientId parameter, and will return data from ARIES for that user's cases
- GetPersonDetails - This method requires a registration parameter, and will return data from EIS and ARIES for that user

### User

This controller is responsible for getting data about the system's current user. 

Method(s) for getting data:

- GetUserInfo - This method takes no parameters, and returns the user's name, group, and userdn, if applicable.

### Status

This controller is responsible for reporting the current status of the Search API.

Method(s) for getting data:

- GetStatus - This method takes no parameters, and returns information on the current status of the Search API, such as Host information, Esb connection, etc.

### Error

This controller handles uncaught exceptions, which are sent to it by .net core.

Methods(s) for getting data:

- Error - Method takes no parameters, and returns relevant information on the error encountered, differing dependent on what environment the application is being run in.