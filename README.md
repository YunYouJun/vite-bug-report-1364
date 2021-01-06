# vite-bug-report-1364

[vitejs/vite #1364 | [Bug report] Can not load file without extname in public folder](https://github.com/vitejs/vite/issues/1364)

## Start

```sh
git clone https://github.com/YunYouJun/vite-bug-report-1364
cd vite-bug-report-1364
yarn
```

```sh
yarn dev
```

## Key Codes

File `src/components/HelloFace.vue` L23

```js
// await faceapi.nets.ssdMobilenetv1.loadFromUri("/models");
await faceapi.nets.ssdMobilenetv1.loadFromUri("/models-with-ext");
```

## Description

I put `ssd_mobilenetv1_model-shard1` & `ssd_mobilenetv1_model-shard2` in `models`, `ssd_mobilenetv1_model-shard1.data` & `ssd_mobilenetv1_model-shard2.data` in `models-with-ext`.

> `ssd_mobilenetv1_model-shard1` is the same as `ssd_mobilenetv1_model-shard1.data`

---

```js
await faceapi.nets.ssdMobilenetv1.loadFromUri("/models-with-ext");
```

This works well.

---

```js
await faceapi.nets.ssdMobilenetv1.loadFromUri("/models");
```

I get this:

```sh
Failed to load url /models/ssd_mobilenetv1_model-shard2. Does the file exist?
Error: Failed to load url /models/ssd_mobilenetv1_model-shard2. Does the file exist?
    at transformRequest (/Users/yunyou/github/pr/vite-bug-report-1364/node_modules/vite/dist/node/chunks/dep-0b3d3f5e.js:66142:15
Click outside or fix the code to dismiss.
You can also disable this overlay with hmr: { overlay: false } in vite.config.js.
```
