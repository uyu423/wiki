---
title: Node.js 및 컴퓨터 비전: 실습 가이드
description: 
published: true
date: 2023-02-09T04:18:36.032Z
tags: 
editor: markdown
dateCreated: 2023-02-09T04:18:29.704Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Node.js and Computer Vision: A Hands-On Guide***English** document is available*](/en/Knowledge-base/Nodejs/node-js-and-computer-vision-a-hands-on-guide)
{.links-list}


# Node.js와 컴퓨터 비전: 실습 가이드

웹 개발 세계에서 Node.js는 널리 사용되는 서버 측 JavaScript 런타임 환경입니다. Netflix, Walmart 및 eBay와 같은 주요 회사에서 사용합니다. 웹 개발만을 위한 것이 아닙니다. Node.js는 데스크탑 애플리케이션 구축 및 임베디드 시스템 개발에도 널리 사용됩니다.

Node.js가 많이 채택되고 있는 한 영역은 컴퓨터 비전입니다. 이 기사에서는 컴퓨터 비전이 무엇인지, Node.js를 사용하여 실습 솔루션을 구축하는 방법을 살펴보겠습니다.

## 컴퓨터 비전이란?

컴퓨터 비전은 컴퓨터가 디지털 이미지를 이해하도록 만드는 방법을 다루는 인공 지능 분야입니다. 여기에는 이미지 인식, 개체 감지 및 이미지 분류와 같은 작업이 포함됩니다.

컴퓨터 비전은 다양한 응용 분야가 있는 광범위한 분야입니다. 자율주행차, 안면인식, 의료영상분석 등에 활용된다.

## Node.js와 컴퓨터 비전

컴퓨터 비전에 Node.js를 사용하는 몇 가지 방법이 있습니다. 가장 인기 있는 두 가지는 오픈 소스 라이브러리인 OpenCV와 상용 라이브러리인 Sightengine입니다.

OpenCV는 가장 널리 사용되는 컴퓨터 비전 라이브러리이며 Node.js를 포함한 많은 프로그래밍 언어에 대한 바인딩이 있습니다. 보안, 로봇 공학 및 증강 현실을 포함한 광범위한 응용 분야에서 사용됩니다.

Sightengine은 이미지 인식에 중점을 둔 상용 컴퓨터 비전 라이브러리입니다. 무료 평가판을 제공하며 Node.js 클라이언트 라이브러리가 있습니다.

이 기사에서는 두 라이브러리 중 더 많이 사용되는 OpenCV에 중점을 둘 것입니다.

## OpenCV 시작하기

OpenCV는 오픈 소스 라이브러리이므로 무료로 설치할 수 있습니다. 가장 쉬운 설치 방법은 Node.js 패키지 관리자인 npm을 사용하는 것입니다.

```
npm install opencv
```

그러면 최신 버전의 OpenCV가 설치됩니다.

OpenCV가 설치되면 Node.js 코드에서 OpenCV를 요구할 수 있습니다.

```javascript
const cv = require('opencv');
```

## 이미지 읽기

컴퓨터 비전 프로젝트의 첫 번째 단계는 이미지를 읽는 것입니다. OpenCV는 `readImage` 함수를 사용하여 이를 쉽게 만듭니다.

```javascript
cv.readImage('image.jpg', (err, img) => {
  if (err) {
    console.error(err);
  } else {
    // Do something with the image
  }
});
```

이미지 `image.jpg`를 읽고 `img` 개체로 제공합니다.

## 이미지 변환

OpenCV는 JPEG, PNG 및 TIFF를 포함한 다양한 이미지 형식을 지원합니다. 그러나 모든 형식이 모든 기능에서 지원되는 것은 아닙니다. 예를 들어 `threshold` 기능은 그레이스케일 이미지만 지원합니다.

이미지를 회색조로 변환하려면 `cvtColor` 함수를 사용할 수 있습니다.

```javascript
cv.cvtColor(img, cv.COLOR_BGR2GRAY, (err, grayImg) => {
  if (err) {
    console.error(err);
  } else {
    // Do something with the grayscale image
  }
});
```

이것은 이미지 `img`를 회색조로 변환하고 `grayImg`로 제공합니다.

## 이미지 임계값 지정

임계값 지정은 컴퓨터 비전에서 일반적인 작업입니다. 이미지를 각 픽셀이 검은색 또는 흰색인 이진 이미지로 변환하는 데 사용됩니다.

OpenCV는 이미지와 임계값을 취하는 `threshold` 함수를 제공합니다. 임계값보다 강도가 높은 픽셀은 흰색으로 변환되고 임계값보다 강도가 낮은 픽셀은 검은색으로 변환됩니다.

```javascript
cv.threshold(grayImg, 127, 255, cv.THRESH_BINARY, (err, binImg) => {
  if (err) {
    console.error(err);
  } else {
    // Do something with the binary image
  }
});
```

이렇게 하면 임계값 127로 이미지 'grayImg'의 임계값이 지정됩니다. 결과 이미지는 'binImg'로 제공됩니다.

## 이미지 반전

어떤 경우에는 이미지를 반전시키는 것이 유용할 수 있습니다. 이것은 `bitwise_not` 함수로 수행할 수 있습니다.

```javascript
cv.bitwise_not(binImg, (err, invImg) => {
  if (err) {
    console.error(err);
  } else {
    // Do something with the inverted image
  }
});
```

이렇게 하면 이미지 `binImg`가 반전되고 결과가 `invImg`로 제공됩니다.

## 이미지 저장

이미지를 처리한 후에는 결과를 저장하고 싶을 것입니다. OpenCV는 이를 위해 `saveImage` 함수를 제공합니다.

```javascript
cv.saveImage('output.jpg', invImg);
```

그러면 이미지 `invImg`가 `output.jpg`로 저장됩니다.

## 결론

이 기사에서는 컴퓨터 비전이 무엇이며 Node.js를 사용하여 실습 솔루션을 구축하는 방법을 살펴보았습니다. OpenCV를 설치하는 방법, 이미지를 읽고 변환하는 방법, 이미지를 임계값으로 지정하는 방법, 이미지를 저장하는 방법을 다뤘습니다.

이것은 컴퓨터 비전과 관련하여 빙산의 일각에 불과합니다. 더 자세히 알아보고 싶다면 아래 리소스를 확인하는 것이 좋습니다.

## 자원

- [OpenCV 문서](https://docs.opencv.org/4.1.0/)
- [Sightengine 설명서](https://sightengine.com/docs/reference/nodejs)
- [Wikipedia의 컴퓨터 비전](https://en.wikipedia.org/wiki/Computer_vision)