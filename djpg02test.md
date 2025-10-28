# What is an API?
An Application Programming Interface (API) is an interface enabling two software applications to talk with each other through requests and responses using a set of protocols and definitions. 

Representational State Transfer (REST) APIs are the most popular and flexible APIs on the modern internet. The client sends data requests to the server. The server uses the received client input to initiate internal functions and returns output data back to the client. REST APIs are stateless meaning servers do not save client data between requests. Client requests to the server are similar to URLs typed in a browser for a website.

The benefits of REST APIs are as follows:
* **Flexibility** - Allows users to communicate back and forth with clients and servers even when hosted on different servers.
* **Adaptability** - Changes to data that resides on the server-side back-end databases are automatically pulled over during the API call without issue because API syntax remains the same.
* **Ease to Understand** - REST architecture helps increase developer productivity with the options to display information on the client-side and store or separately manipulate the data on the server-side.

<figcaption><p align="center"><strong>Figure 1 - Basic API Flow</strong></p></figcaption>

# Key Parts of an API
An API is a set of programmable instructions that allow two applications to communicate. Below are the fundamental components required to ensure the data is correctly called for and received.

### API Client
Simplifies the use of the API while shielding the user from the backend technical intricacies. An API client can also initiate a request or an external event from a service or application that automatically activates a request. 

### API Key
A unique passcode containing numbers and letters that grants access to an API. The keys improve security, authenticate an application, or identify an authorized user. 

### API Requests
A message (or a call) sent to an application server asking for a specific service, functionality, or data. The sub-components that make up REST API requests are:

| **Term** | **Definition** |
|-----------|----------------|
| **Endpoint** | The location where an API receives requests for data and functionality, typically represented by Uniform Resource Locators (URLs). The endpoint lets different systems and applications communicate by sending and receiving instructions. |
| **Request Method** | Specific operations the client wants to perform on the URL resource (e.g., GET, POST, PUT, DELETE). |
| **Parameters** | Variables passed to an endpoint to provide instructions the API server needs to process. The parameters are typically included as part of the request in the URL string or the request body field. |
| **Request Headers** | Provides essential information for a server to process the request. This information can include metadata such as content type, authentication tokens, and other data required by the server or client to process the response or request. |
| **API Server** | A type of intermediary software that sits between different systems and allows different applications to communicate. |
| **API Response** | The generated response returned to the client. A response may include the following components: status code, response headers, and body. |
<figcaption><p align="center"><strong>Table 1 - Key API Terms</strong></p></figcaption>