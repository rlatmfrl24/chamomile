---
title: Firebase init 401 error 대처법
date: "2019-09-02T00:00:11.210Z"
template: "post"
draft: false
slug: "/posts/Firebaes-init-401-error-대처법/"
category: "Boilerplate"
tags:
  - "Firebase"
  - "Boilerplate"
description: "Node.js 환경에서 Firebase init 수행시 OAuth 획득 과정에서 401 에러가 발생하는 경우가 있다.</br>
Firebase Documentation에서의 안내대로 `firebase login`을 수행해도 정상적으로 로그인되어있다고 나오지만,</br>
`firebase init`을 수행해도 마찬가지 401 에러가 나온다."
socialImage: ""
---

Node.js 환경에서 Firebase init 수행시 OAuth 획득 과정에서 401 에러가 발생하는 경우가 있다.</br>
Firebase Documentation에서의 안내대로 `firebase login`을 수행해도 정상적으로 로그인되어있다고 나오지만,</br>
`firebase init`을 수행해도 마찬가지 401 에러가 나온다.

이 경우에는 다음과 같이 재로그인을 통해 **Firebase CLI** 접근 권한을 취득해주면 해결된다.

> firebase loing --reauth
