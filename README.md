# svelte-with-scss
svelte 시작 템플릿에 scss를 에러없이 사용하기 위한 환경셋팅 적용.

## 추가한 모듈
- <a href="https://www.npmjs.com/package/@rollup/plugin-alias" target="_blank">@rollup/plugin-alias</a>
- <a href="https://www.npmjs.com/package/sass" target="_blank">sass</a>
- <a href="https://www.npmjs.com/package/svelte-preprocess" target="_blank">svelte-preprocess</a>
- <a href="https://www.npmjs.com/package/rollup-plugin-scss" target="_blank">rollup-plugin-scss</a>
- <a href="https://www.npmjs.com/package/path" target="_blank">path</a>

---

## 설치된 모듈 설명
- **@rollup/plugin-alias, path**: 기본 소스 경로를 설정할 수 있게 합니다.
```js
// rollup.config.js
export default {
  ...
  plugins: [
    ...
    alias({
      entries: [
        { find: '@', replacement: path.resolve(__dirname, 'src') }
      ]
    ...
    }),
  ...
```
```js
// Before
import Button from '../../components/Button.svelte';

// After
import Button from '@/components/Button.svelte';
```
- **svelte-preprocess, sass**: svelte에 SCSS를 사용할 수 있습니다.
```js
// svelte.config.js
const sveltePreprocess = require('svelte-preprocess');
const production = !process.env.ROLLUP_WATCH;

module.exports = {
  dev: !production,
  preprocess: sveltePreprocess(),
}
```
```scss
<style lang="scss">
@import "src/assets/styles/base/variables";
.wrap-contents {
  max-width: 640px;
  margin: 0 auto;
  background-color: $color-white;
}
</style>
```
- **rollup-plugin-scss**: SCSS파일 import 플러그인 입니다. `main.js`에서 임포트한 `.scss`를 글로벌 스타일시트로 빌드 할 수 있습니다.
```js
// main.js
import '@/assets/styles/app.scss';
import App from '@/App.svelte';

const app = new App({...
```
```js
// rollup.config.js
export default {
...
  plugins: [
    ...
    scss({
      output: 'public/global.css'
    }),
    ...
```
---
## 패키지 설치, 개발환경 실행
```
npm i
npm run dev
```
