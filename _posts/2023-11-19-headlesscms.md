 Headless CMS
 Contest Management System(컨텐츠 관리 시스템)의 약자입니다.
 그럼 여기에서 Headless는 무엇이냐.
 웹 개발을 사람 몸으로 비유하자면 body를 backend라고 많이 일컫고요.
 나라는 사람을 보여주는 얼굴을 Frontent라고 합니다.
 그럼 여기에서 Headless라는 것은 less는 무언가가 없다는 것이니
 "머리가 없는"이라는 뜻이에요.
 그럼 웹개발에서 Headless라는 것은 "프론트앤드가 없는 컨텐츠 관리 시스템"을 의미합니다.

 웹개발에서 body부분, 데이터를 저장하는 것을 담당하는 것을 CMS라고 합니다.
 Body부분을 그러니까 데이터를 어떻게 나타낼건지는 전혀 관여하지 않기 때문에
 프런트엔드를 우리가 원하는대로 자유자재 바꿔서 보여줄 수 있어요.

> Headless CMS is a back end-only web content management system that acts primarily as a content repository.
> Headless CMS란 백엔드만 가지고 있는 웹 컨텐츠 관리 시스템의 약자로 주로 컨텐츠를 보관하고 있는 저장소 역할을 한다.
> A headless CMS makes content accessible via an API for display on any device, without a built-in front end or presentation layer.
> headless CMS는 프론트앤드가 없는 컨텐츠 관리 시스템이니까 데이터를 일고 쓰고 관리하기 위해서는 API를 거쳐서 사용해야합니다.

이것을 sanity에서 재미있게 설명하고 있습니다.
> A headless CMS is a content management system that separates where content is stored (the "body") from where it is presented (the "head").
> headless CMS이란 컨텐츠 관리 시스템으로 body(컨텐츠가 어디에 저장되어 있는지)와 Head(그것을 어디에서 보여줄건지)를 잘 분리해 둔 것입니다.
> It separateds infromation and presentation.
> 데이터를 읽고 쓰고 업데이트하고 관리하는 부분만 담당하고 있으니까 presentation layer와 data layer를 분리했습니다.
> this enables content reuse and remixing across web, mobile, and digital media platforms as needed.
> You could even reuse your content in print.

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/aa99526f-b01b-4231-98cf-86bf9a8a738d)
예전 전통적인 방식의 (Head가 있는)CMS에는 데이터를 저장하는 것뿐만 아니라 어떻게 표기할건지를 당당하고 있었습니다.
Headless CMS는 data layer가 어떻게 보여질건지와는 분리되어 있고 데이터를 저장하고 변경하기 위해서는 API를 사용해야 합니다.
API를 형태로 데이터를 읽고 쓰고 변경할 수 있기 때문에 rendering을 어디에서 어떤 방식으로 할건지는 자유자재로 우리가 결정해서 사용할 수 있습니다.
그 말은 즉, API만 사용하면 웹, 앱, 데스크 탑 어플리케이션도 만들 수 있습니다.
어떻게 UI를 보여줄건지는 headless CMS는 관리하지 않습니다.
대표적인 headless CMS를 살펴보면 WordPress는 전통적인 CMS로 유명하지만 최근에 headless CMS도 지원해주고 있습니다.
그다음으로 많이 사용하는 것이 Strapi입니다. Strapi는 headless CMS에서 sanity와 막강하게 유명합니다.
오픈소스이기 때문에 strapi 소스를 다운받아서 내가 원하는대로 커스터마이징해서 그것을 AWS에 호스팅하면
나만의 CMS를 사용할 수 있어요.
최근에는 strapi도 클라우드 형태의 서비스를 제공해주고 있습니다. 예전에는 strapi를 받아서 개발자 스스로 호스팅 해야한다는 부담감이 있었는데요.
이제는 조금 더 간편하게 사용해볼 수 있을거같아요.
그래서 strapi는 클라우드 시장에 뛰어든지는 얼마되지 않았습니다.
클라우드 시장에서 오랫동안 점유율을 차지한 것이 바로 sanity입니다.
sanity는 오픈소스가 아니기때문에 직접 소스코드를 확인할 수 없고 그들만의 클라우드 서비스를 사용해야 합니다.

# sanity의 동작원리
![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/cd613bbb-9b31-45ab-8786-8daa25543515)
우리가 sanity를 이용해서 데이터를 저장하면 Content Lake라는 클라우드에 데이터가 저장 됩니다.
그 클라우드에 있는 데이터를 읽고 쓰기 위해서 두가지 방법이 있습니다.
1. 개발자 모드인 Sanity Studio를 통해서 하는 것입니다.
   데이터의 골격을 결정할 수 있는 문서(어떤 스키마에 데이터를 저장할건지)와 저장된 데이터를 시각적으로 확인하고 편집까지 할 수 있는 관리자용 콘솔 UI모드가 있습니다.
   sanity에서 제공해주는 Sanity Studio를 이용해서 데이터를 직접 관리할 수 있습니다.
2. sanity에서 제공해주는 API를 사용해서 우리 어플리케이션에서 데이터를 직접 읽고 쓸 수 있습니다.

 어떻게 데이터의 골격을 결정할 수 있는지
 어떻게 관리자 콘솔을 잘 사용할 수 있는지에 대해서도 다뤄보고
 우리 어플리케이션에서도 데이터를 읽고 쓸때 어떻게 sanity에 접속하는 것이 가장 개발자 다운, 안정성이 높은 것인지 얘기해보겠습니다. 
