---
title: JSBarcode 安装
---

# JSBarcode 安装

## 通过NPM安装

使用NPM安装JSBarcode是最推荐的方式，特别是在现代前端项目中：

```bash
npm install jsbarcode
```

安装完成后，可以在JavaScript文件中导入：

```javascript
// 导入完整库
import JsBarcode from 'jsbarcode';

// 或者按需导入特定格式
import { CODE128 } from 'jsbarcode/src/barcodes';
```

## 通过CDN引入

如果你不使用构建工具，可以通过CDN直接在HTML中引入JSBarcode：

```html
<!-- 使用jsDelivr CDN -->
<script src="https://cdn.jsdelivr.net/npm/jsbarcode@3.11.6/dist/JsBarcode.all.min.js"></script>

<!-- 或使用unpkg CDN -->
<script src="https://unpkg.com/jsbarcode@3.11.6/dist/JsBarcode.all.min.js"></script>
```

## 下载文件手动引入

你也可以从GitHub仓库下载最新的发布版本，然后手动引入到你的项目中：

1. 访问 [JSBarcode GitHub Releases](https://github.com/lindell/JsBarcode/releases)
2. 下载最新版本的压缩文件
3. 解压并将`dist`目录中的文件复制到你的项目中
4. 在HTML中引入：

```html
<script src="path/to/JsBarcode.all.min.js"></script>
```

## 不同版本说明

JSBarcode提供了几种不同的构建版本，可以根据需要选择：

- **JsBarcode.all.min.js**: 包含所有条形码类型的完整库（推荐）
- **JsBarcode.all.js**: 未压缩的完整库，包含所有条形码类型
- **JsBarcode.min.js**: 仅包含CODE128条形码类型的最小库
- **单独的条形码类型文件**: 在`dist/barcodes`目录下可以找到单独的条形码类型文件

## 在不同环境中使用

### 在Vue.js中使用

```javascript
import JsBarcode from 'jsbarcode';

export default {
  mounted() {
    JsBarcode("#barcode", "Hello World")