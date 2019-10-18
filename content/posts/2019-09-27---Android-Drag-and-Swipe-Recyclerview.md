---
title: Android Drag and Swipe Recyclerview
date: "2019-09-27T00:00:11.210Z"
template: "post"
draft: false
slug: "/posts/Android-Drag-and-Swipe-Recyclerview/"
category: "Boilerplate"
tags:
  - "Android"
  - "Recyclerview"
  - "Drag"
  - "Swipe"
description: "RecyclerView에서 대표적으로 활용되는 Interaction Gesture는 Drag와 Swipe가 있다. 이와 관련된 유용한 Article이 있기에 정리해둔다."
socialImage: ""
---

## Drag and Swipe RecyclerView

RecyclerView에서 대표적으로 활용되는 Interaction Gesture는 Drag와 Swipe가 있다. 이와 관련된 유용한 Article이 있기에 정리해둔다.

[Drag and Swipe RecyclerView](http://dudmy.net/android/2018/05/02/drag-and-swipe-recyclerview/)

## Interaction 관련 내용 추가

RecyclerView에 Drag 동작시 해당 Item를 강조하고 싶은 경우가 있다.
이런 경우를 위해선 RecyclerView에 적용되는 ItemTouchListener를 Custom 해줘야한다.
