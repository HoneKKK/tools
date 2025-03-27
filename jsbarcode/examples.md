---
title: JSBarcode 使用示例
---

# JSBarcode 使用示例

## 基础示例

以下是一个基础的条形码生成示例：

```html
<!DOCTYPE html>
<html>
<head>
  <title>JSBarcode 基础示例</title>
</head>
<body>
  <svg id="barcode"></svg>
  
  <script src="https://cdn.jsdelivr.net/npm/jsbarcode@3.11.6/dist/JsBarcode.all.min.js"></script>
  <script>
    // 生成 CODE128 条形码
    JsBarcode("#barcode", "Hello World!", {
      format: "CODE128",
      width: 2,
      height: 100,
      displayValue: true
    });
  </script>
</body>
</html>
```

## 多种格式示例

以下示例展示了不同类型的条形码格式：

```html
<!DOCTYPE html>
<html>
<head>
  <title>JSBarcode 多种格式示例</title>
  <style>
    .barcode-container {
      margin-bottom: 20px;
    }
    .barcode-label {
      font-family: Arial, sans-serif;
      font-size: 14px;
      margin-bottom: 5px;
    }
  </style>
</head>
<body>
  <div class="barcode-container">
    <div class="barcode-label">CODE128:</div>
    <svg class="barcode" id="code128"></svg>
  </div>
  
  <div class="barcode-container">
    <div class="barcode-label">EAN13:</div>
    <svg class="barcode" id="ean13"></svg>
  </div>
  
  <div class="barcode-container">
    <div class="barcode-label">CODE39:</div>
    <svg class="barcode" id="code39"></svg>
  </div>
  
  <div class="barcode-container">
    <div class="barcode-label">UPC:</div>
    <svg class="barcode" id="upc"></svg>
  </div>
  
  <div class="barcode-container">
    <div class="barcode-label">ITF14:</div>
    <svg class="barcode" id="itf14"></svg>
  </div>
  
  <script src="https://cdn.jsdelivr.net/npm/jsbarcode@3.11.6/dist/JsBarcode.all.min.js"></script>
  <script>
    // CODE128
    JsBarcode("#code128", "Hello World!", {
      format: "CODE128",
      width: 2,
      height: 80,
      displayValue: true
    });
    
    // EAN13
    JsBarcode("#ean13", "5901234123457