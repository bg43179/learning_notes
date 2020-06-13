# API Design

# http method

PUT: Method only allows a complete replacement of a document.

PATCH: modify an existing HTTP resource.

DELETE: <br>
respones: 204 no content

# Http Headers

- `Accept`: Informs the server about the types of data that can be sent back.
  Ex:<br/>
  `Accept: 'application/vnd.api+json'` is for json api<br/>
  `Accept: 'application/json'` is for regular json<br/>
