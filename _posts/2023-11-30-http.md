- 1xx: Information
  - 100: Continue
  - 102: Processing
- 2xx: Success
  - 200: OK
  - 201: Created
  - 204: No Content(요청은 처리했고 거기에 대한 컨텐츠는 없어)
- 3xx: Redirection
  - 301: Moved Permanently(니가 요청한 페이지는 영구적으로 옮겨졌어)
  - 302: Found(니가 요청한 페이지 임시적으로 여기로 이동했어)
  - 303: See Other(302와 비슷한데 get요청에서 사용)
  - 307: Temporary Redirect(임시적으로 리다이렉트)
  - 308: Permanent Redirect(영구적으로 리다이렉트)
- 4xx: Client error
  - 400: Bad Request
  - 401: Unauthorized
  - 403: Forbidden
  - 404: Not Found
  - 405: Method Not Allowed(해당 url에 대해 쓰거나 삭제하는 기능이 없을때)
  - 409: Conflict(사용자가 생성하려는 소스코드가 이미 있거나 충돌이 발생)
- 5xx: Server error
  - 500: Internal Server Error
  - 502: Bad Gateway
  - 503: Service Unavailable

서버에서 클라이언트에 Response를 보낼 때 header에 Set-Cookie를 보냅니다.
클라이언트에서 서버에 api를 요청할 때 브라우저에서 자동으로 Cookie를 추가해서 보냅니다.

또, 서버에서 Response를 보낼 header에 cache-control을 보내어 캐시의 보관기간을 보낼 수 있습니다.
브라우저는 자동으로 브라우저 저장소에 이 데이터를 저장해두었다가 저장된 데이터를 재활용하게 됩니다.
서버에서 요청하는 클라언트가 누구인지 알 수 있는 User-Agent도 있습니다.

Headers에는 Standard와 Custom이 있습니다.
Custom은 domain-key, domain.key로 키의 이름을 지을 수 있습니다.

클라이언트에서 보내주는 Request Header의 종류
- User-Agent
- Authorization

서버에서 보내주는 Response header의 종류
- Content-Length : 컨텐츠가 얼마나 큰지 사이즈(bytes)에 대한 정보
- Content-Type: text/html|application/json 컨텐츠 타입에 대한 정보
- Content-Language: en 언어에 대한 정보
- Cahce-Content: 서버에서 클라이언트에게 얼마나 오랫동안 데이터를 캐시해야하는지 명시할 수도 있습니다.
  ```
  Cache-Control:max-age=<seconds>
  Cache-control:no-cache
  ```
  
