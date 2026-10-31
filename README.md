# battery-pack-miniprogram

UniApp + Vue 3 微信小程序示例，使用 npm 包 `antbms-battery-pack` 展示电池包电压、温度与均衡状态。

## 使用

```bash
npm install
npm run dev:mp-weixin
```

用微信开发者工具导入 `dist/dev/mp-weixin`，并在 `src/manifest.json` 的 `mp-weixin.appid` 填入你自己的小程序 AppID。

## 发布

```bash
npm run build:mp-weixin
```

用微信开发者工具导入 `dist/build/mp-weixin`，上传开发版本并提交审核。

## 数据接入

修改 `src/pages/index/index.vue` 中的 `refresh()`，把示例随机数据替换为你的 BMS 接口数据。数据字段包括 `id`、`voltage`、`temperature`、`status`、`passiveBalance` 和可选的 `activeBalance`。
