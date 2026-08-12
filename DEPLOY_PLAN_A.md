# 《拯救甜恩静麦克风计划》方案 A 上线说明

## 目标

采用“Vercel 海外/默认入口 + 国内备用入口”的方式上线。

- Vercel：用于快速上线、海外访问、马来西亚粉丝访问、日常预览。
- 国内备用：用于保障中国内地粉丝访问稳定性，可选腾讯云 COS、阿里云 OSS、CloudBase 静态托管。
- 粉丝站：先放默认入口和备用入口；后续如果支持 iframe，可以内嵌我们的游戏页。

## 当前项目结构

上线时至少需要这些文件：

- `index.html`
- `assets/audio/roly-poly.mp3`
- `assets/characters/states/**`
- `assets/hands/catch-hands.png`
- `assets/ui/life.png`
- `vercel.json`

不建议上传：

- `assets/audio/roly-poly.flac`

`roly-poly.flac` 文件较大，当前页面实际使用的是 `roly-poly.mp3`。

## Vercel 主站

推荐步骤：

1. 新建一个 GitHub 仓库，例如 `eunjung-mic-game`。
2. 上传干净部署包里的所有文件。
3. 登录 Vercel，选择该 GitHub 仓库导入。
4. Framework 选择 `Other` 或保持默认静态项目识别。
5. Build Command 留空。
6. Output Directory 留空或使用根目录。
7. 部署后拿到 `https://xxx.vercel.app` 地址。
8. 用手机和微信内置浏览器测试打开、播放音乐、接麦手感。

## 国内备用入口

可选平台：

- 腾讯云 COS 静态网站
- 阿里云 OSS 静态网站
- CloudBase 静态托管

推荐步骤：

1. 使用同一份干净部署包。
2. 上传 `index.html` 和 `assets` 目录。
3. 开启静态网站托管。
4. 配置默认首页为 `index.html`。
5. 开启 HTTPS。
6. 用国内手机网络测试加载速度和音频播放。

## 粉丝站接入方式

第一版建议用按钮跳转：

```html
<a href="https://你的-vercel-地址" target="_blank" rel="noopener">
  点击进入《拯救甜恩静麦克风计划》
</a>
```

如果希望更一体，可以让管理员尝试 iframe：

```html
<iframe
  src="https://你的游戏地址"
  style="width: 100%; height: 720px; border: 0; border-radius: 16px; overflow: hidden;"
  allow="autoplay; fullscreen"
  loading="lazy">
</iframe>
```

手机专题页可以使用满屏 iframe：

```html
<div style="position: relative; width: 100%; height: 100vh; overflow: hidden;">
  <iframe
    src="https://你的游戏地址"
    style="position: absolute; inset: 0; width: 100%; height: 100%; border: 0;"
    allow="autoplay; fullscreen">
  </iframe>
</div>
```

## 推荐发布文案

默认入口：

```text
点击进入《拯救甜恩静麦克风计划》
```

备用入口：

```text
如果打不开或加载较慢，请点击国内备用入口。
```

## 上线前检查

- 手机微信内置浏览器能打开。
- 点击开始后 BGM 可以播放。
- 四位角色素材正常加载。
- 接麦手图正常显示。
- 生命值图片正常显示。
- Game Over、连击、难度提升、比心、哭泣状态都正常。
- Vercel 地址和国内备用地址都能访问。
