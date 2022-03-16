---
title: "go语言校验密码强度"
date: 2022-03-16T14:32:47+08:00
description:
# weight: 1
# aliases: ["/first"]
draft: false
author: "嘟囔"
# author: ["Me", "You"] # multiple authors
tags: ["go"]
categories: ["go"]
---

go语言校验密码复杂度的函数，大写、小写、数字、特殊字符。

```go

package main

import (
	"regexp"
    "strings"
)

const (
	levelD = iota
	LevelC
	LevelB
	LevelA
	LevelS
)
 
func checkPasswd(minLength, maxLength, minLevel int, pwd string) bool {
	if len(pwd) < minLength {
		return false
	}
	if len(pwd) > maxLength {
		return false
	}
 
	var level int = levelD
	patternList := []string{`[0-9]+`, `[a-z]+`, `[A-Z]+`, `[~!@#$%^&*?_-]+`}
	for _, pattern := range patternList {
		match, _ := regexp.MatchString(pattern, pwd)
		if match {
			level++
		}
	}
 
	if level < minLevel {
		return false
	}
	return true
}

fun main() {
    isOk := checkPasswd(8, 64, LevelS, myWindow.passwd.Text())
    if(!isOk) {
        myWindow.showConfigErr(" 密码错误！") //或者打印出来
        return
    }
}
```