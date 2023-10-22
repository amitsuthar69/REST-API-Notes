### Some important Response object methods (res.)

|     Method      | Description                                                      |
| :-------------: | ---------------------------------------------------------------- |
|    res.send     | sends a response back to client                                  |
|    res.json     | sends a response in JSON format                                  |
|   res.render    | renders an HTML view / file                                      |
|  res.redirect   | redirects the client to different URL                            |
|  res.sendFile   | sends a files as response to client                              |
|   res.status    | sets the HTTP status code for response                           |
|   res.cookie    | sets a cookie in client's browser                                |
| res.clearCookie | clears the previously set cookie                                 |
|  res.setHeader  | sets an individual HTTP header for the response                  |
|     res.set     | allows setting multiple HTTP headers in a single call            |
|     res.get     | retrieves the value of an HTTP header from the request           |
|   res.locals    | pass data to view trmplate engine                                |
|     res.end     | ends the response process                                        |
|  res.download   | initiate a fioe download                                         |
|    res.type     | sets the Content-Type header for the response                    |
|   res.format    | Performs content negotiation based on the client's Accept header |
