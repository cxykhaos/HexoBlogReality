---
title: Grpc常见问题
date: 2021-12-10 15:40:24
categories: 
           - Golang
tags:
           - Grpc
           - Golang
---

Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues).

# Grpc常见问题

## 问题1

```protobuf
protoc-gen-go: unable to determine Go import path for "Prod.proto"
```

## 解决方法

```protobuf
option go_package="./;khaosgrpc"; 
##后面那个是包名
```

