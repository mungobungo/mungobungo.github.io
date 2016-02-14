---
layout: post
title:  "installin neuromindic with caffe and torch and stuff"
date:   2016-02-12 23:41:12 +0100
categories: machine_learning deep_learning caffe torch
---

usually guys that play with deep learning using caffe tool
caffe is deep leraning framework
can see what it is here

http://caffe.berkeleyvision.org/tutorial/

But there's more. Ready trained neural networks for many deep-learning machine vision tasks

https://github.com/BVLC/caffe/wiki/Model-Zoo

everything started with
```
docker pull kaixhin/cuda-torch
```

hopefully it would work

took a long time...

```
Using default tag: latest
latest: Pulling from kaixhin/cuda-torch
bbe1c4256df3: Pull complete 
911d09728ffd: Pull complete 
615765bc0d9f: Pull complete 
a3ed95caeb02: Pull complete 
f6c40ea017da: Pull complete 
a53854637f3f: Pull complete 
14ced4e3a4ff: Pull complete 
1fd3da14976b: Pull complete 
ae360da3a5a7: Pull complete 
9ea528cd9401: Extracting 71.86 MB/216.5 MB
b64c1d772908: Download complete 
22d75ad8602c: Download complete 

```

and after it was completed, added Docke file 
and 

```
docker build .
```

it succeeded.
so here we go further

```
$docker tag 10a7b2fc0bca mungobungo/neuromindic:0.1

$ docker login
Username (mungobungo): 
Password: 
WARNING: login credentials saved in /home/vagrant/.docker/config.json
Login Succeeded

$ docker push mungobungo/neuromindic:0.1

```
