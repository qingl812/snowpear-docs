# vue

- vue 下载 `npm install -g @vue/cli`

## Element ui

- Element ui 下载 `npm i element-ui -S`

```typescript
// main.ts
import "element-ui/lib/theme-chalk/index.css";
import ElementUI from "element-ui";

Vue.use(ElementUI);
```

# router

```typescript
// router.ts
const routes: Array<RouteConfig> = [
 {
  path: "*",
  component: () => import("../views/WithHead.vue"),
  children: [
   {
    path: "/home",
    component: () => import("../views/Home.vue"),
    meta: {
     title: "道路信息管理系统 - 主页",
    },
   },
  ],
 },
 {
  path: "*",
  name: "NotFound",
  component: () => import("../views/NotFound.vue"),
 },
];

// main.ts
import { NavigationGuardNext, Route } from "vue-router";

router.beforeEach((to: Route, from: Route, next: NavigationGuardNext) => {
 /* 路由发生变化修改页面title */
 if (to.meta?.title) {
  document.title = to.meta.title;
 }
 next();
});
```

## 后端数据模拟 mockjs

```shell
npm install mockjs
npm install @types/mockjs
```

## axios

```shell
npm install axios
npm install @types/axios
```

# npm

## 临时使用

```shell
npm --registry https://registry.npm.taobao.org install express
```

## 持久使用

```shell
npm config set registry https://registry.npm.taobao.org
```

## 验证

```shell
npm config ls
npm config get registry
npm info express
```

## 更新

```shell
npm install -g npm
```
