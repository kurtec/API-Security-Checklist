(中文版请戳这:[中文版](https://github.com/GrayLand119/API-Security-Checklist/blob/master/README-zh.md))

# API Security Checklist
Checklist of the most important security countermeasures when designing, testing, and releasing your API.

------------------------------------------------------------------------------
## Authentication
- [x] Don't use `Basic Auth` Use standard authentication (e.g. JWT, OAuth).
- [x] Don't reinvent the wheel in `Authentication`, `token generating`, `password storing` use the standards.

### JWT (JSON Web Token)
- [ ] Use random complicated key (`JWT Secret`) to make brute forcing token very hard.
- [ ] Don't extract the algorithm from the payload. Force algorithm in the backend (`HS256` or `RS256`). 
- [x] Make token expiration (`TTL`, `RTTL`) as short as possible.
- [x] Don't store sensitive data in the JWT payload, it can be decoded [easily](https://jwt.io/#debugger-io).

### OAuth
- [ ] Always validate `redirect_uri` on server side to allow only whitelisted URLs.
- [x] Always try to exchange for code not tokens (don't allow `response_type=token`).
- [ ] Use `state` parameter with a random hash to prevent CSRF on OAuth authentication process.
- [x] Define default scope, and validate scope parameter for each application. 

## Access
- [ ] Limit requests (Throttling) to avoid DDoS / Bruteforce attacks.
- [x] Use HTTPS on server side to avoid MITM (Man In The Middle Attack).
- [ ] Use `HSTS` header with SSL to avoid SSL Strip attack.

## Input
- [x] Use proper HTTP method according to operation , `GET (read)`, `POST (create)`, `PUT (replace/update)` and `DELETE (to delete a record)`.
- [x] Validate `content-type` on request Accept header ( Content Negotiation ) to allow only your supported format (e.g. `application/xml` , `application/json` ... etc) and respond with `406 Not Acceptable` response if not matched.
- [x] Validate `content-type` of posted data as you accept (e.g. `application/x-www-form-urlencoded` , `multipart/form-data ,application/json` ... etc ).
- [x] Validate User input to avoid common vulnerabilities (e.g. `XSS`, `SQL-Injection` , `Remote Code Execution` ... etc).
- [x] Don't use any sensitive data ( `credentials` , `Passwords`, `security tokens`, or `API keys`) in the URL, but use standard Authorization header.

## Processing
- [x] Check if all endpoint protected behind the authentication to avoid broken authentication.
- [x] User own resource id should be avoided. Use `/me/orders` instead of `/user/654321/orders`
- [ ] Don't use auto increment id's use `UUID` instead.
- [x] If you are parsing XML files, make sure entity parsing is not enabled to avoid `XXE` (XML external entity attack).
- [x] If you are parsing XML files, make sure entity expansion is not enabled to avoid `Billion Laughs/XML bomb` via exponential entity expansion attack.
- [ ] Use CDN for file uploads.
- [ ] If you are dealing with huge amount of data, use Workers and Queues to return response fast to avoid HTTP Blocking. 
- [x] Do not forget to turn the DEBUG mode OFF.

## Output
- [ ] Send `X-Content-Type-Options: nosniff` header.
- [ ] Send `X-Frame-Options: deny` header.
- [ ] Send `Content-Security-Policy: default-src 'none'` header.
- [ ] Remove fingerprinting headers - `X-Powered-By`, `Server`, `X-AspNet-Version` etc.
- [x] Force `content-type` for your response , if you return `application/json` then your response `content-type` is `application/json`.
- [x] Don't return sensitive data like `credentials` , `Passwords`, `security tokens`.
- [x] Return the proper status code according to the operation completed. (e.g. `200 OK` , `400 Bad Request` , `401 Unauthorized`, `405 Method Not Allowed` ... etc).


------------------------------------------------------------------------------

# Contribution
Feel free to contribute , fork -> edit -> submit pull request. For any questions drop us an email at team@shieldfy.io.
