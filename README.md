# uni-vue3-ts-template
uni-app Vue3 + TypeScript + Vite + Pinia + Unocss 模板项目

## Env Suggest
**Node >= 18**

**pnpm 8**

**Registry taobao - https://registry.npmmirror.com/**

## Use This Template
```sh
npx degit atqq/uni-vue3-ts-template#main my-uni-vue3-ts-vite-project
```
## Feature
### Prod
* [x] [Vue3](https://vuejs.org/)
* [x] [Pinia](https://pinia.vuejs.org/) - replace vuex
* [x] [Axios](https://github.com/axios/axios)
* UI/组件库
  * [x] [uView](https://vkuviewdoc.fsq.pub/) - vk-uview-ui
  * [ ] [uni-ui](https://github.com/dcloudio/uni-ui) - 待接入
### Dev
* [x] [Vite](https://github.com/vitejs/vite)
* [x] [TypeScript](https://github.com/microsoft/TypeScript/#readme)
* [x] [Sass](https://github.com/sass/sass)
* [x] [Less](https://github.com/less/less.js)
* [x] [Eslint](https://eslint.org/)
* [x] [Prettier](https://prettier.io/)
* [x] [Vitest](https://vitest.dev/) - replace jest
* [x] [unocss](https://github.com/unocss/unocss) - 即时按需原子 css 引擎
* [x] GitHooks [simple-git-hooks](https://github.com/toplenboren/simple-git-hooks#readme)
* ~~LintStaged~~
* ~~StyleLint~~

## 使用
### 安装依赖
**建议使用pnpm，依赖安装速度更快**
```sh
npm i -g pnpm
```

```sh
pnpm install
```

**MAC M1(ARM芯片)，其它操作系统无需关注**，正常运行需要手动安装 `esbuild-darwin-64`即可
```sh
pnpm add @esbuild/darwin-x64@0.18.20 -D
```
安装的版本或者指令可以运行下面这个脚本获取
```sh
node arm-esbuild-version.js
```
![](https://img.cdn.sugarat.top/mdImg/MTY5NDk1ODQ0Njk1Ng==694958446956)


## 本地启动
### 微信小程序
```sh
# 构建出产物
pnpm dev:mp-weixin
```

### H5
```sh
# CSR
pnpm dev:h5
```

## 打包构建
### 微信小程序
```
pnpm build:mp-weixin
```
### H5
```sh
# CSR
pnpm build:h5
```

## 别名配置

如果我们想要在`import`的时候 src 的路径简写成`@`，下面的就是配置 vite 的别名，[属性类型请查看vite文档](https://vitejs.cn/config/#resolve-alias)

- `@` 代替 `./src`
- `@components`代替`./src/components`

```typescript
// vite.config.ts
export default defineConfig({
  // ......
  resolve: {
    alias: {
      '@': path.resolve(__dirname, './src'),
      '@components': path.resolve(__dirname, './src/components')
    }
  }
})
```

例子：

```diff
// pages/index/index.vue
- import Hello from '../../components/hello/index.vue'
+ import Hello from '@/components/hello/index.vue'
// 或者
+ import Hello from '@components/hello/index.vue'
```

### ts

如果是使用ts开发，这样还不够，ts不会识别路径的别名，显示找不到模块的报错，这个时候需要修改 `tsconfig.json` 文件，纠正下路径才可以。



```diff
// tsconfig.json
{
  // ......
  "compilerOptions": {
    // ......
+    "baseUrl": "./",
+    "paths": {
+      "@/*": ["src/*"],
+      "@components/*": ["src/components/*"]
    }
  },
}

```

添加 `baseUrl` 和 `paths` 参数，就可以完美解决编辑器的报错提示了！