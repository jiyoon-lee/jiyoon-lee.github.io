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
