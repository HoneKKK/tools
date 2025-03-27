---
title: JSBarcode API参考
---

# JSBarcode API参考

## 基本语法

JSBarcode的基本语法如下：

```javascript
JsBarcode(element, text, [options]);
```

### 参数说明

- **element**: 要渲染条形码的DOM元素或选择器
- **text**: 要编码的文本内容
- **options**: 可选的配置选项对象

## 选择器语法

JSBarcode支持多种方式选择要渲染的元素：

```javascript
// 使用CSS选择器
JsBarcode("#barcode", "Hello");

// 使用DOM元素
var element = document.getElementById("barcode");
JsBarcode(element, "Hello");

// 使用jQuery选择器（如果有jQuery）
JsBarcode($("#barcode"), "Hello");

// 选择多个元素
JsBarcode(".barcode", "Hello");
```

## 配置选项

JSBarcode提供了丰富的配置选项来自定义条形码的外观和行为：

```javascript
JsBarcode("#barcode", "Hello", {
  // 条形码类型
  format: "CODE128",
  
  // 线条宽度
  width: 2,
  
  // 条形码高度
  height: 100,
  
  // 显示文本
  displayValue: true,
  
  // 文本字体
  font: "monospace",
  
  // 文本对齐方式
  textAlign: "center",
  
  // 文本位置
  textPosition: "bottom",
  
  // 文本边距
  textMargin: 2,
  
  // 字体大小
  fontSize: 20,
  
  // 背景色
  background: "#ffffff",
  
  // 线条颜色
  lineColor: "#000000",
  
  // 边距
  margin: 10,
  
  // 条形码旋转角度（度）
  rotate: 0,
  
  // 是否扁平化SVG路径
  flat: false,
  
  // 渲染完成回调函数
  onSuccess: function(instance) {},
  
  // 渲染失败回调函数
  onError: function(error) {},
  
  // 是否有效（用于验证）
  valid: function(valid) {}
});
```

## 支持的条形码格式

JSBarcode支持多种条形码格式，可以通过`format`选项指定：

| 格式 | 描述 | 有效字符 | 示例 |
|------|------|----------|-------|
| CODE128 | 高密度条形码，支持所有ASCII字符 | ASCII字符 | `JsBarcode('#barcode', 'Hello', {format: 'CODE128'});` |
| CODE128A | CODE128 A模式，支持大写字母和控制字符 | 大写字母, 数字, 控制字符 | `JsBarcode('#barcode', 'ABC123', {format: 'CODE128A'});` |
| CODE128B | CODE128 B模式，支持所有可打印ASCII字符 | 所有可打印ASCII字符 | `JsBarcode('#barcode', 'Hello World!', {format: 'CODE128B'});` |
| CODE128C | CODE128 C模式，支持数字（每两位数字为一组） | 数字（偶数位） | `JsBarcode('#barcode', '12345678', {format: 'CODE128C'});` |
| EAN13 | 国际商品编码，13位数字 | 数字（12位+1位校验码） | `JsBarcode('#barcode', '5901234123457', {format: 'EAN13'});` |
| EAN8 | 缩短版EAN码，8位数字 | 数字（7位+1位校验码） | `JsBarcode('#barcode', '96385074', {format: 'EAN8'});` |
| UPC | 通用产品代码，12位数字 | 数字（11位+1位校验码） | `JsBarcode('#barcode', '123456789999', {format: 'UPC'});` |
| CODE39 | 支持字母、数字和特殊字符 | 大写字母, 数字, 特殊字符 | `JsBarcode('#barcode', 'ABC-123', {format: 'CODE39'});` |
| ITF14 | 物流包装用条码，14位数字 | 数字（偶数位） | `JsBarcode('#barcode', '10012345678902', {format: 'ITF14'});` |
| MSI | 主要用于仓库管理 | 数字 | `JsBarcode('#barcode', '123456', {format: 'MSI'});` |
| MSI10 | MSI带模10校验 | 数字 | `JsBarcode('#barcode', '123456', {format: 'MSI10'});` |
| MSI11 | MSI带模11校验 | 数字 | `JsBarcode('#barcode', '123456', {format: 'MSI11'});` |
| MSI1010 | MSI带双模10校验 | 数字 | `JsBarcode('#barcode', '123456', {format: 'MSI1010'});` |
| MSI1110 | MSI带模11和模10校验 | 数字 | `JsBarcode('#barcode', '123456', {format: 'MSI1110'});` |
| pharmacode | 制药行业使用的条码 | 数字（1-9999） | `JsBarcode('#barcode', '1234', {format: 'pharmacode'});` |
| codabar | 早期用于图书馆和医疗系统 | 数字, 特殊字符 | `JsBarcode('#barcode', 'A12345B', {format: 'codabar'});` |

## 方法链

JSBarcode支持方法链式调用，可以在同一个元素上生成多个条形码：

```javascript
JsBarcode("#barcode")
  .options({font: "OCR-B"}) // 设置所有条形码的选项
  .CODE128("ABC", {height: 50})
  .blank(20) // 添加空白
  .EAN13("5901234123457", {fontSize: 18, textMargin: 0})
  .render(); // 最后调用render方法进行渲染
```

## 验证

JSBarcode提供了验证功能，可以检查输入的数据是否有效：

```javascript
JsBarcode("#barcode", "123456789", {
  format: "EAN13",
  valid: function(valid) {
    if (valid) {
      console.log("条形码有效");
    } else {
      console.log("条形码无效");
    }
  }
});
```

## 错误处理

可以通过`onError`回调函数处理渲染错误：

```javascript
JsBarcode("#barcode", "123", {
  format: "EAN13", // EAN13需要12位数字+1位校验码
  onError: function(error) {
    console.log(error);
  }
});
```

## SVG导出

如果你需要导出SVG代码，可以使用以下方法：

```javascript
var svg = document.getElementById("barcode");
var svgText = new XMLSerializer().serializeToString(svg);
```

## Canvas渲染

JSBarcode也支持在Canvas上渲染条形码：

```javascript
var canvas = document.getElementById("barcode");
JsBarcode(canvas, "Hello", {
  format: "CODE128",
  width: 2,
  height: 100
});
```