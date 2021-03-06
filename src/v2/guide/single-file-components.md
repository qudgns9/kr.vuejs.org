---
title: 싱글 파일 컴포넌트
type: guide
order: 401
---

## 소개

<div class="vueschool"><a href="https://vueschool.io/lessons/introduction-to-single-file-components?friend=vuejs" target="_blank" rel="sponsored noopener" title="Free Vue.js Single File Components lesson">Watch a free video lesson on Vue School</a></div>

많은 Vue 프로젝트에서, 전역 컴포넌트는 `Vue.component`를 사용해 정의되고, 다음에 모든 페이지의 container 엘리먼트를 대상으로 하는 `new Vue({el: '#container'})`가 정의됩니다.

이것은 특정 뷰를 향상시키는 용도로만 사용되는 중소 규모 프로젝트에서 유용합니다. 하지만 좀 더 복잡한 프로젝트의 경우 또는 프론트엔드가 JavaScript 기반인 경우 단점이 분명해집니다.

- **전역 정의** 모든 구성 요소에 대해 고유한 이름을 지정하도록 강요됩니다.
- **문자열 템플릿** 구문 강조가 약해 여러 줄로 된 HTML에 보기 안좋은 슬래시가 많이 필요합니다.
- **CSS 지원 없음** HTML 및 JavaScript가 컴포넌트로 모듈화 되어 있으나 CSS가 빠져 있는 것을 말합니다.
- **빌드 단계 없음** Pug (이전의 Jade) 및 Babel과 같은 전처리기가 아닌 HTML 및 ES5 JavaScript로 제한됩니다.

위 모든 것들은 Webpack 또는 Browserify와 같은 빌드 도구를 이용해 `.vue` 확장자를 가진 **싱글 파일 컴포넌트** 로 해결 됩니다.

다음은 `Hello.vue` 파일의 간단한 예입니다.

<a href="https://gist.github.com/chrisvfritz/e2b6a6110e0829d78fa4aedf7cf6b235" target="_blank" rel="noopener noreferrer"><img src="/images/vue-component.png" alt="Single-file component example (click for code as text)" style="display: block; margin: 30px auto;"></a>

이제 우리는 할 수 있습니다:

- [완전한 구문 강조](https://github.com/vuejs/awesome-vue#source-code-editing)
- [CommonJS 모듈](https://webpack.js.org/concepts/modules/#what-is-a-webpack-module)
- [컴포넌트에만 제한된 CSS](https://github.com/vuejs/vue-loader/blob/master/docs/en/features/scoped-css.md)

약속대로 Jade, Babel (ES2015 모듈을 포함합니다), Stylus와 같은 전처리기를 사용해 더 깨끗하고 기능이 풍부한 컴포넌트를 사용할 수 있습니다.

<a href="https://gist.github.com/chrisvfritz/1c9f2daea9bc078dcb47e9a82e5f7587" target="_blank" rel="noopener noreferrer"><img src="/images/vue-component-with-preprocessors.png" alt="Single-file component example with preprocessors (click for code as text)" style="display: block; margin: 30px auto;"></a>

이러한 특정 언어는 예제일 뿐입니다. Bublé, TypeScript, SCSS, PostCSS 또는 생산성 향상에 도움을 주는 다른 전처리기를 쉽게 사용할 수 있습니다. Webpack을 `vue-loader`와 함께 사용하면 CSS 모듈에 대한 1등급 클래스를 지원합니다.

### 관심사의 분리는 무엇입니까?

주목해야 할 중요한 점은 **관심사 분리가 파일 타입 분리와 같지 않다는 것입니다.** 현대적인 UI 개발에서 코드베이스를 서로 얽혀있는 세 개의 거대한 레이어로 나누는 대신, 느슨하게 결합 된 컴포넌트로 나누고 구성하는 것이 더 중요합니다. 컴포넌트 내부에서 템플릿, 로직 및 스타일이 본질적으로 결합되어 배치되면 컴포넌트의 응집력과 유지 보수성이 향상됩니다.

싱글 파일 컴포넌트에 대한 아이디어가 마음에 들지 않더라도 JavaScript와 CSS를 별도의 파일로 분리하여 핫 리로드 및 사전 컴파일 기능을 활용할 수 있습니다.

``` html
<!-- my-component.vue -->
<template>
  <div>이 곳은 사전에 컴파일 됩니다.</div>
</template>
<script src="./my-component.js"></script>
<style src="./my-component.css"></style>
```


## 시작하기

### 예제 샌드박스

지금 당장 싱글 파일 컴포넌트를 사용하고 싶다면 CodeSandbox의 [단순한 할일 앱](https://codesandbox.io/s/o29j95wx9)을 확인하세요.


### JavaScript에서 모듈 빌드 시스템을 처음 사용하는 사용자를 위한 내용

`.vue` 컴포넌트로, 우리는 진보한 JavaScript 영역에 들어서고 있습니다. 약간의 아직 배우지 않은 추가 도구 사용방법을 배워야 합니다.

- **Node Package Manager (NPM)** :  [시작 안내서]((https://docs.npmjs.com/packages-and-modules/getting-packages-from-the-registry))에서 어떻게 레지스트리에서 패키지를 가져오는지 읽어보세요.
- **ES2015/16를 사용하는 최신 JavaScript** : Babel의 [ES2015 교육 가이드](https://babeljs.io/docs/learn-es2015/)를 읽어보세요. 지금 당장 모든 기능을 외울 필요는 없으나 이 페이지는 언제든지 다시 볼 수 있도록 가지고 계세요.

위 내용을 얻으려면 하루정도 걸립니다. 이 후에 [Vue CLI 3](https://cli.vuejs.org/) 를 확인하는 것을 추천합니다. 설명을 따라 가면 `.vue` 컴포넌트, ES2015 및 핫 리로드가 포함된 Vue 프로젝트를 즉시 사용할 수 있게 됩니다.

템플릿은 여러 "모듈"을 가져와 최종 응용프로그램에 묶는 모듈 번들러인 [Webpack](https://webpack.github.io/)을 사용합니다. Webpack 자체에 대한 자세한 내용을 보려면 [이 동영상](https://www.youtube.com/watch?v=WQue1AN93YU)에서 좋은 소개를 볼 수 있습니다. 일단 기본을 익히면 [Egghead.io의 고급 Webpack 코스](https://egghead.io/courses/using-webpack-for-production-javascript-applications)과 [Webpack Academy](https://webpack.academy/p/the-core-concepts)를 확인하십시오.

### 고급 사용자를 위한 내용

The CLI takes care of most of the tooling configurations for you, but also allows fine-grained customization through its own [config options](https://cli.vuejs.org/config/).

In case you prefer setting up your own build setup from scratch, you will need to manually configure webpack with [vue-loader](https://vue-loader.vuejs.org). To learn more about webpack itself, check out [their official docs](https://webpack.js.org/configuration/) and [Webpack Academy](https://webpack.academy/p/the-core-concepts).
