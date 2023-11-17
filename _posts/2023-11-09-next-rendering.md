
# SSG
```javascript
export async function generateStaticParams() {
  // 모든 제품의 페이지들을 미리 만들어 둘 수 있게 해줍니다.(SSG)
  const proudcts = await getProducts();
  return proudcts.map((product, index) => ({
    slug: product.id,
  }));
}
```
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/be7c0e23-12db-4554-8009-faefb9d4c18a)


# ISR
참고: https://nextjs.org/docs/pages/building-your-application/data-fetching/incremental-static-regeneration
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/b4b9d357-fbfa-4c6a-ba3f-1bb8edbaa148)
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/8badd5d9-47c1-49d4-a1a6-bd343bf5d6af)
```
npm run build
npm run start
```
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/248c9bbc-5ed3-4484-a3b4-dca88b5add78)
3초 후에 페이지를 새로고침하면 텍스트가 변경된 것을 확인할 수 있습니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/1b72082a-e152-4572-a88c-6b481a7ad354)

자, 이제는 fetch를 이용해서 api조회를 해보겠습니다.
```javascript
https://meowfacts.herokuapp.com // 사용할 api
```
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/70e3618e-99dc-4257-a0b2-917e0f1e43ab)
`npm run build && npm run start`를 실행해보면 이상합니다. revalidate를 3으로 해두었기 때문에 3초에 한번씩 api를 호출할 것이라 생각했지만
그렇지않습니다. 왜 안되는지 이유를 잘 모르겠습니다. 의도된 현산이라는 말도 있고 어차피 사용하지않을 기능이라는 말도 있네요.
이번에는 revalidate를 fetch의 속성으로 주도록 하겠습니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/1a18e627-1dc5-4ac2-89b1-cb6a4ea7c783)
fetch의 속성으로 주어도 똑같이 작동되야합니다...
이번에는 revalidate를 0으로 바꿔보겠습니다. 그러면 이제 페이지를 새로고침할 때마다 테스트가 바뀝니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/350c930b-577b-4d4e-871c-ced78d4c7f43)
SSR로 바뀌어 페이지를 요청할 때마다 revalidate합니다(HTML을 새로만듭니다)
revalidate를 0으로 해도 SSR이 되고 `no-store`로 해도 SSR이 됩니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/2ea6de5a-2d40-4a77-bc1b-57e813e25475)


# CSR
CSR로 만들기위해서는 클라이언트 컴포넌트에서 API를 호출하면 됩니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/51884c6e-679a-45ff-9ced-38a1e027b008)
그러면 페이지를 새로고침할때마다 api를 호출하는 것을 확인할 수 있습니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/32833dd3-ad60-441f-a969-d7901026d748)
또한 서버로 부터 받은 정적 HTML에도 초기 설정한 text인 '데이터 준비중...'을 확인할 수 없습니다.
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/aaf59e6a-a7e9-4d8b-88a5-bfc63c7d3235)
이렇듯 Next는 모든 파일들을 돌아다니면서 정적 HTML로 만들 수 있는 것은 미리 다 만들어놓습니다.
이후에 만약 어떤 소스가 클라이언트 컴포넌트라면 이 부분만 클라이언트에게 보내주고 클라이언트에서 hydration이 일어나면 이벤트가 실행되고 업데이트되는 원리입니다.
