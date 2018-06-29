# Lemage — 一个为图片而生的lib

### 0. 项目说明

​	Lemage是一款图片选择器组件，为了能让开发者用尽可能少的代码实现尽可能美观的图片选择相关的控件，目前整个组件包含**相册照片选择**、**相机拍照**、**图片预览**三部分。

​	很多开发者为了方便，无论是图片选择、还是调用相机进行拍照，都直接调用了系统的相册和相机，但是Android中机型复杂，本身就UI长相大不相同，造成了不同手机上用户体验的不一致，更别说iOS和Android的UI风格统一了。但是要让开发者去写一套完整的相册照片选择、相机拍照、图片预览的功能的话，也的确太耗费工时，会增加很多开发上的时间成本，所以一套成型、美观、各平台UI风格一致的组件看来还是挺有必要存在的。我们的Team也遇到了上述问题，为了方便自己，也方便大家，将此部分源码特意整理成Lib库开放出来，供大家使用，也希望大家能够对控件多多支持，发现问题及时告诉我们，让我们一起来让它变得更好。

![LemageLogo](https://raw.githubusercontent.com/LemonITCN/lemage-design/master/Lemage.png)

### 1. 功能介绍

#### 1.1. LemageURL说明

- 格式：lemage://图片来源/图片分类/图片标识
- 图片来源：图片来源目前分为两种
  - 相册 album：所有从相册中获取到的图片都属于此来源
  - 沙盒 sandbox：相机拍照、通过UIImage生成的LemageURL都属于此来源
- 图片分类：
  - 相册来源目前只有一种分类：local
  - 沙盒来源目前有两种分类：长期有效 long ， 短期有效 short，相机拍照产生的LemageURL属于短期有效的分类
- URL举例：
  - 相册中的图片：lemage://album/local/AA39A4B6-8777-424F-963E-3E40583C8971/L0/001 
  - 沙盒中的长期图片：lemage://sandbox/long/ed7e24d7-a1f2-45a9-8737-1132c094baf9
  - 沙盒中的短期图片：lemage://sandbox/short/eac56594-567f-44e9-bbae-38299718d714

#### 1.1. 照片选择器



通过PHImageManager获取到所有照片的PHAsset对象，拿到PHAsset的localIdentifier字符串

缩略图通过这个方法获取300*300的CGSize的图片

```objective-c
- (PHImageRequestID)requestImageForAsset:(PHAsset *)asset 
    						  targetSize:(CGSize)targetSize 
                             contentMode:(PHImageContentMode)contentMode 
                                 options:(nullable PHImageRequestOptions *)options 
                           resultHandler:(void (^)(UIImage *__nullable result, NSDictionary *__nullable info))resultHandler;
```

lemage://album/