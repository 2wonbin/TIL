# SASS 초기화
> 이 게시글엔 [김버그님의 SASS 강의](https://edu.goorm.io/lecture/25681/%EA%B9%80%EB%B2%84%EA%B7%B8%EC%9D%98-ui-%EA%B0%9C%EB%B0%9C-%EB%B6%80%ED%8A%B8%EC%BA%A0%ED%94%84-%EA%B2%BD%EB%A0%A5%EA%B0%99%EC%9D%80-%EC%8B%A0%EC%9E%85%EC%9C%BC%EB%A1%9C-%EB%A0%88%EB%B2%A8%EC%97%85) 내용 일부가 포함되어 있습니다.<br />
> 문제가 될 경우 게시물은 삭제됩니다. 


### 브라우저별, 태그별 가지고 있는 속성값들을 다루기 쉽게 초기화 과정을 가진다.
<hr/>

### Nomalize.css
[[Nomalize.css 다운로드]](https://necolas.github.io/normalize.css/8.0.1/normalize.css) 에서 문서를 다운받아 CSS에 적용한다.

### Custom
자신의 선호에 맞는 요소들을 추가하여 사용한다.

### <예시>
``` css
* {
  margin: 0; //여전히 H1태그는 margin이 적용 ->nomalize css에서 h1태그에 적용
  font-family: 'Noto Snas KR', sans-serif;
  box-sizing: border-box;
}

html {
  font-family: 'Noto Snas KR', sans-serif;
}

body {
  font-family: 'Noto Snas KR', sans-serif; // font가 유달리 적용이 안될 경우엔 전체 / html / body까지 지정해주자.
}

h1 {
  margin: 0; //그래서 h1자체에 margin을 없애버린다.
}

a {
  color: inherit; //inherit : 해당 태그가 속해있는 요소의 color값을 그대로 상속받겠다.
  text-decoration: none;
}

/* Form 태그 초기화*/
button,
input,
select,
textarea {
  background-color: transparent;
  border: 0;

  &:focus {
    //sass 문법 '&'(상위요소참조) : AND, 선언한 요소 내부 추가 설정을 원할 경우 
    outline: none;
    box-shadow: none;
  }
}

a,
button {
  //굳이 hover 설정을 안해도 된다.
  cursor: pointer;
}

/*목록 태그 초기화*/
ul,
ol {
  padding-left: 0;
  list-style: none;
}

```

## 추가설정

``` JSON
/* package.json*/
"scripts": {
    ....
    "sass": "node-sass -wr --source-map true styles/main.scss style.css"
  },
```
**'--source-map'** 옵션을 *true*로 설정해 chrome 개발자 도구에서 sass 파일을 직접 확인할 수 있도록 한다.