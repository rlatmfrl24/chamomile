---
title: Android RecyclerView Data Observer
date: "2019-10-17T00:00:11.210Z"
template: "post"
draft: false
slug: "/posts/Android-RecyclerView-Data-Observer/"
category: "Boilerplate"
tags:
  - "Android"
description: ""
socialImage: ""
---

이번에는 RecyclerView에서 데이터가 변경될 시에 별도의 동작이나 기능을 추가하고 싶을 때 사용하는 클래스이다. 좀더 원론적으로 보자면 RecyclerView Adapter의 데이터를 Observing한다고 보면 된다.

```
adapter.registerAdapterDataObserver(object : RecyclerView.AdapterDataObserver(){
  override fun onChanged(...) { ... }
  override fun onItemRangeChanged(...) { ... }
  override fun onItemRangeInserted(...) { ... }
  override fun onItemRangeMoved(...) { ... }
  override fun onItemRangeRemoved(...) { ... }
})

```
