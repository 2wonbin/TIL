# 중첩(Nesting) 
[[참조: Sass완전정복]](https://heropy.blog/2018/01/31/sass/)

## 기존 css에서
``` css
.nav {
  width: 100%;
}
.nav .list {
  padding: 20px;
}
.nav .list li {
 list-style: none;
}
```

### 다른 방법이 없을까?

## Sass에서는
``` scss
.nav {
  width: 100%;
  .list {
    padding: 20px;
    li {
      list-style: none;
    }
  }
}
```
<hr />

## 상위 선택자
## Sass
``` Scss
.button{
  width: 100px;
  height: 100px;
  color: red;
  
  &:hover{       //상위 선택자의 블록 내부에 '&' 키워드로 그대로 가져온다.
    color: blue;  // .button:hover { color : blue}
  }
}
```

<hr />

## 중첩 벗어나기
> 같은 변수를 공유하고 싶지만 '관계'에 얽히고 싶지 않을 경우 '@at-root' 사용한다
``` scss
.list {
  $w: 100px;
  $h: 50px;
  li {
    width: $w;
    height: $h;
  }
  @at-root .box {   //li 태그 하위의 .box 가 아닌 독립적인 요소로서, 단지 선언한 변수의 값만 가져온다.
    width: $w;
    height: $h;
  }
}

```

<hr />

## 속성의 중첩
> 'OOO-XXX' 형태의 속성들을 묶어서 관리할 수 있다.
``` Scss
.box {
  border: {
    top: 1px dotted #000000;
    radius: 1em;
  };
}
``` 

## 🙌주의사항
### 중첩은 깊게들어가지 말라. [[참조: 코드 중첩은 4레벨 보다 깊게 들어가지 말 것]](https://velopert.com/1712)