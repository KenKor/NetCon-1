---
title: NetCon TraceMode Enumerator
description: Determines the way tracing algorithms can walk through the network.
permalink: 
aliases: 
draft: false
date: 2025-04-19
tags: 
---
# NetCon TraceMode Enumerator

Enumerator that determines the way tracing algorithms can walk through the network.
The enumerator partially works as flags, e.g. normal+backwards=any and, down+up=mazed.

|  Id | Name      | Description                                                                                                 |
| --: | --------- | ----------------------------------------------------------------------------------------------------------- |
|   1 | normal    | Follow connections in the order from FromId to ToId and reversed if bidirectional.                          |
|   2 | backwards | Opposite of 'normal'; unidirectional connections are traversed in the opposite direction.                   |
|   3 | any       | Ignore directionality of the connections.                                                                   |
|   4 | down      | Follow flow downstream flow (as determined by barriers, commodity rules and flow restrictions).             |
|   8 | up        | Follow flow upstream flow (as determined by barriers, commodity rules and flow restrictions).               |
|  12 | mazed     | Follow flow upstream or downstream flow (as determined by barriers, commodity rules and flow restrictions). |
