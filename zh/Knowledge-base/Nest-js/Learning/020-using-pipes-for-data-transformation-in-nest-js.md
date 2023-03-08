---
title: 020: 在 Nest.js 中使用管道进行数据转换
description: 
published: true
date: 2023-02-09T15:17:23.631Z
tags: 
editor: markdown
dateCreated: 2023-02-09T15:17:21.913Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [020: Using pipes for data transformation in Nest.js***English** document is available*](/en/Knowledge-base/Nest-js/Learning/020-using-pipes-for-data-transformation-in-nest-js)
{.links-list}


# 在 Nest.js 中使用管道进行数据转换

在 Nest.js 中，管道用于数据转换。管道将数据作为输入，并将转换后的数据作为输出返回。

管道可用于多种任务，例如：

- 验证
- 格式化
- 转型

可以使用 @Pipe 装饰器创建管道。 `@Pipe` 装饰器将管道的名称作为参数。

```javascript
@ Pipe({
  name: 'myPipe'
})
```

可以使用 .pipe() 方法将管道链接在一起。 `.pipe()` 方法将管道名称作为参数。

```javascript
.pipe(myPipe)
```

管道可用于 Nest.js 控制器和服务。要在控制器中使用管道，可以使用 @UsePipes 装饰器。 `@UsePipes` 装饰器将管道名称作为参数。

```javascript
@ UsePipes(myPipe)
```

要在服务中使用管道，可以使用 .usePipe() 方法。 `.usePipe()` 方法将管道的名称作为参数。

```javascript
.usePipe(myPipe)
```

## 创建管道

要创建管道，可以使用 @Pipe 装饰器。 `@Pipe` 装饰器将管道的名称作为参数。

```javascript
@ Pipe({
  name: 'myPipe'
})
```

管道必须有一个 transform() 方法。 `transform()` 方法将要转换的数据作为参数接收并返回转换后的数据。

```javascript
transform(data: any) {
  return data;
}
```

## 链接管道

可以使用 .pipe() 方法将管道链接在一起。 `.pipe()` 方法将管道名称作为参数。

```javascript
.pipe(myPipe)
```

## 在控制器中使用管道

管道可用于 Nest.js 控制器和服务。要在控制器中使用管道，可以使用 @UsePipes 装饰器。 `@UsePipes` 装饰器将管道名称作为参数。

```javascript
@ UsePipes(myPipe)
```

## 在服务中使用管道

要在服务中使用管道，可以使用 .usePipe() 方法。 `.usePipe()` 方法将管道的名称作为参数。

```javascript
.usePipe(myPipe)
```

## 例子

在此示例中，将创建一个管道，它接收一个字符串并返回所有大写字母的字符串。

```javascript
@ Pipe({
  name: 'uppercasePipe'
})
export class UppercasePipe implements PipeTransform {
  transform(data: string) {
    return data.toUpperCase();
  }
}
```

该管道可以像这样在控制器中使用：

```javascript
@ Controller('/')
@ UsePipes(UppercasePipe)
export class MyController {
  @ Get('/')
  getData(@ Req() request: Request) {
    return {
      data: 'Hello, world!'
    };
  }
}
```

## 附加信息

- [Nest.js 管道](https://docs.nestjs.com/pipes)
- [Nest.js UsePipes](https://docs.nestjs.com/use-pipes)

## 警告

- 管道按照它们被链接的顺序执行。

## 危险

- 如果管道抛出错误，管道链的执行将停止。