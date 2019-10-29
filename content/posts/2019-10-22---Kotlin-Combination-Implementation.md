---
title: 면접질문 관련 메모 정리
date: "2019-10-22T00:00:11.210Z"
template: "post"
draft: false
slug: "/posts/면접질문-관련-메모-정리/"
category: ""
tags:
  - "Kotlin"
  - "Combination"
  - "Algorithm"
description: "코틀린을 활용한 알고리즘 문제를 풀다가 조합을 활용할 일이 많아서 이를 정리해두기 위한 클래스를 간략히 짜보았다."
socialImage: ""
---

코틀린을 활용한 알고리즘 문제를 풀다가 경우의 수와 관련된 문제들이 자주 나와서 이를 쉽게 풀어나가기 위한 클래스를 만들어 보았다. 필요할 때가 활용하면 유용할 것 같다.


```
class CaseFactory(val valueList: Array<String>){
    private val visit = BooleanArray(valueList.size)
    private var caseResult = mutableListOf<List<String>>()
    private var combinationFlag = false
    private var targetSize = 0

    fun setCombinationFlag(value: Boolean){
        combinationFlag = value
    }

    fun setTargetSize(value: Int){
        targetSize = value
    }

    fun build(): List<List<String>>{
        caseResult.clear()
        if (targetSize <= valueList.size){
            if (combinationFlag){
                combination(valueList, visit, 0, valueList.size, targetSize)
            }
            else {
                permutation(valueList, 0, valueList.size, targetSize)
            }
        }
        return caseResult
    }

    private fun permutation(array: Array<String>, depth:Int, n: Int, r: Int){
        if (depth==r){
            val list = array.toList().take(r)
            caseResult.add(list)
            return
        }
        else {
            for (i in depth until n){
                array[i] = array[depth].also { array[depth] = array[i] }
                permutation(array, depth+1, n, r)
                array[i] = array[depth].also { array[depth] = array[i] }
            }
        }
    }

    private fun combination(arr: Array<String>, visited: BooleanArray, index: Int, n: Int, r: Int){
        if (r == 0){
            val result = mutableListOf<String>()
            for (i in visited.indices){
                if (visited[i]) result.add(arr[i])
            }
            caseResult.add(result)
        }
        else {
            for (i in index until n){
                visited[i] = true
                combination(arr, visited, i+1, n, r-1)
                visited[i] = false
            }
        }
    }
}
```


