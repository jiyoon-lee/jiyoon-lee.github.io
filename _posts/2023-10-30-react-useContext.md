---
layout: single
title: "39장 DOM"
categories: javascript
tag: [python, blog]
toc: true
author_profile: false
sidebar:
  nav: "docs"
toc: true
---

Context를 사용하면 데이터를 부모로부터 직접 전달받지 않아도 컴포넌트가 필요한 데이터를 참조할 수 있습니다.
예를 들어, 로그인한 사용자 정보를 어느 컴포넌틍도 참조할 수 있는것과 같습니다.

사용방법을 알아보겠습니다.<br>
`components`폴더에 `ContextSample.tsx`파일을 만들겠습니다.<br>
Consumer와 Provider를 사용합니다.
Provider를 이용해 Context를 설정하고, Consumer를 이용해 Context 값을 참조합니다.

```javascript
import React from "react";

// Title을 전달하기 위해 Context를 작성합니다.
const TitleContext = React.createContext("");

const Title = () => {
  return (
    <TitleContext.Consumer>
      {/* Consumer 바로 아래 함수를 두고, Context를 참조합니다. */}
      {(title) => {
        return <h1>{title}</h1>;
      }}
    </TitleContext.Consumer>
  );
};

const Header = () => {
  return (
    <div>
      {/* Header에서 Title로는 아무런 데이터를 전달하지 않습니다. */}
      <Title />
    </div>
  );
};

const Page = () => {
  const title = "React Book";

  return (
    <TitleContext.Provider value={title}>
      <Header />
    </TitleContext.Provider>
  );
};

export default Page;
```

![image](https://github.com/jiyoon-lee/jiyoon-lee.github.io/assets/59562141/bd90c75f-d196-41c3-8479-ea46f38a3ce8)
