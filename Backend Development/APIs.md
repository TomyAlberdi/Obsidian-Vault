Created: 2024-09-28 19:20
## Family Tree:
1. Computer
2. [[Backend Development]]
-- -
An **Application Programming Interface (API)** is essentially a URL that, when accessed, returns information for another system to consume, instead of a web page. In other words, APIs are developed so that two systems can communicate with each other.
APIs can be **public**, **private**, or **semi-public**:
- **Public APIs**: These do not require anything to be consumed. Example: **RESTCountries**.
- **Semi-public APIs**: These require the user to register and generally have usage limits. Example: **Twitter API**.
- **Private APIs**: These are not accessible to the public, as they are typically used within organizations. Example: **Netflix**.
## Endpoint
An **endpoint** is a connection point that we target to get the information we need. It refers to the specific URLs we use to retrieve data from a server via an API. Each endpoint represents a specific resource or function of the API.
## RESTful
**RESTful** refers to a web service that implements the **REST (Representational State Transfer)** architecture. Key characteristics of RESTful services include:
- **Client-server architecture**: Separates the client from the server.
- **Based on HTTP protocol**: Uses standard HTTP methods.
- **Stateless**: The server does not store any client context between requests.
- **Resource-based**: Access resources via a URL.
### HTTP Methods used in RESTful APIs:
- **GET**: Retrieves data from the server (read operations).
- **POST**: Creates new records on the server.
- **PUT**: Updates an existing record.
- **DELETE**: Deletes an existing record.
### Examples of popular RESTful APIs:
- **[Facebook](https://developers.facebook.com/)**
- **[Cloudways]( [https://www.cloudways.com/blog/introducing-cloudways-api/)**
- **[Twitter]( [https://dev.twitter.com/rest/public)**
- **[Google Translate](https://cloud.google.com/translate/docs/translating-text](https://cloud.google.com/translate/docs/translating-text)**
### JSON:
In RESTful services, responses to requests are typically returned in a data exchange format that both the client and server can understand, usually **XML** or **JSON**.
**JSON (JavaScript Object Notation)** is a lightweight text format for data exchange. It's easy for humans to read and write, and it's also simple for machines to parse and generate.
```json
{  
  "nombre": "Homer",
  "apellido": "Simpson",
  "sons": ["Bart", "Lisa", "Maggie"],
  "age": 40,
  "wife": true
}
```
In this example:
- **Strings** are enclosed in double quotes.
- **Arrays** (e.g., "sons") are enclosed in square brackets.
- **Booleans** (e.g., "wife") and **numbers** (e.g., "age") do not require quotes.
![[json-back-c25-3.jpg]]