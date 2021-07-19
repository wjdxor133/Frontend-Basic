## SSR(Server Side Rendering)

- `서버 사이드 렌더링`은 `서버 측에서 HTML을 만들어 클라이언트로 보내주는 것`을 말한다.
- 페이지가 이동할 때마다 새로고침이 일어나며 새로운 페이지를 요청한다.
- 즉, 페이지에서 요청 시 마다 서버로부터 리소스를 받아 해석하고 화면에 렌더링하는 방식이다.

### 👍🏻 장점

- 초기 페이지 로드가 빠르다.
- 자바스크립트 코드가 동작하기 전에도 완성된 형태의 템플릿 (HTML에 데이터가 삽입된 상태)을 서버로 부터 전달받기 때문에 검색로봇이 페이지를 크롤링하기에 매우 적합하다.
- 때문에 검색 엔진 최적화(SEO)에 유리하다.
- 정적 사이트에 적합하다.

### 👎🏻 단점

- 매번 페이지를 요청할때 마다 새로고침이 발생하기 때문에, 새로운 페이지를 이동하면 화면이 ‘깜빡’인다. (UX 관점에서 불편함)
- 매번 페이지 요청할 때 마다 불필요한 템플릿도 중복해서 로딩하여 서버의 트래픽을 매우 불필요하게 낭비될 수 있기 때문에 성능에 좋지 않다.
- 서버와의 잦은 응답으로 서버에 부담이 간다.

## CSR(Client Side Rendering)

- `클라이언트 사이드 렌더링`은 최초의 서버에서 `전체 페이지`를 받아서 보여준다.
- 이후에는 사용자의 요청에 따라, 리소스를 서버에서 제공받아 렌더링하는 방식을 말한다.
- 즉, 서버는 단지 JSON 파일만 보내주는 역할을 하며, 나머지는 클라이언트 측에서 JSON 데이터를 가지고 화면을 그려주는 방식이다.
- 그래서 최근에 이러한 방식 적목 시킨 것을 `**SPA(Single Page Application)**`라고 하며 많이 사용되어지고 있다.

## SPA(Single Page Application)

- 오랫동안 웹 개발에서 웹 사이트를 화면에 표시하는 유일한 방법은 서버 사이드 렌더링(SSR) 방식이었다.
- 하지만 모바일 시대가 도래하면서 모바일 환경에 최적화된 서비스가 분명 필요해졌다.
- 그래서 나온 개념이 `**SPA(Single Page Application)**`이다.
- 말 그대로 `**하나의 페이지로 구성된 애플리케이션**`을 말한다.
- SPA는 웹 사이트가 로딩될 때 필요한 모든 정적 리소스를 딱 `**한번만**` 받아온다.
- 모든 페이지를 다운 받았기 때문에 그 이후에는 새로운 페이지 요청이 있을 때 혹은 데이터 변경이 일어났을 때 페이지 갱신에 필요한 데이터만 서버로 부터 전달 받아서 페이지를 다시 렌더링한다.
- 그렇기 때문에 SPA는 `**CSR(Client Side Rendering) 방식으로 렌더링을 한다`\*\* 라고 볼수 있다.

### 👍🏻 장점

- 사용자의 행동에 따라 필요한 부분만 다시 읽어들이기 때문에 빠른 인터랙션이 가능하며, UX 관점에서 사용자에게 최적화된 환경을 제공한다.
- 요청 시 마다 필요한 리소스만 받아서 렌더링하기 때문에 트래픽이 감소되고, 서버 부하가 덜하다.
- 모바일 웹 개발에서는 동일한 백엔드 데이터를 재사용이 가능하다.

### 👎🏻 단점

- 한번에 리소스 파일들을 모두 받아오기 때문에 초기 페이지 로드 속도가 오래 걸리고 느리다.
- 대부분의 웹 크롤러 봇들은 자바스크립트 파일을 실행시키지 못하면 빈 페이지로 인식하기 때문에 검색 엔진 최적화(SEO)에 불리하다.

## 🚀 결론

CSR 방식과 SSR 방식을 적절히 잘 섞어서 사용하면 더 좋은 어플리케이션을 만들수 있다.

## ✔️ 참고

[CSR(Client Side Rendering) 과 SSR(Server Side Rendering) / SPA, MPA](https://kyoung-jnn.tistory.com/entry/CSRClient-Side-Rendering-%EA%B3%BC-SSRServer-Side-Rendering)

[](https://inmediatum.com/en/blog/innovacion1/who-is-better-ssr-aplication-vs-spa-aplication/)

[SSR vs CSR vs SPA](https://devgaram.github.io/966ea5b2cd8e89dbab1723a18bec85539cbfa10a)

[서버 사이드 렌더링(SSR)과 클라이언트 사이드 렌더링(CSR)](https://goodgid.github.io/Server-Side-Rendering-and-Client-Side-Rendering/)

[CSR vs SSR (클라이언트 사이드 렌더링과 서버사이드 렌더링)](https://imkh.dev/csr-ssr/)

[[10분 테코톡] 🍻주모의 SPA](https://www.youtube.com/watch?v=vM_zQLnlyKw)

[SPA vs MPA와 SSR vs CSR 장단점 뜻정리 | 하나몬](https://hanamon.kr/spa-mpa-ssr-csr-%EC%9E%A5%EB%8B%A8%EC%A0%90-%EB%9C%BB%EC%A0%95%EB%A6%AC/)
