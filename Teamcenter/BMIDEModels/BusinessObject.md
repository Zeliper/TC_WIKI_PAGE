---
title: BusinessObject
description: 
published: true
date: 2023-07-10T09:57:09.272Z
tags: 
editor: markdown
dateCreated: 2023-07-10T09:57:09.272Z
---

# BusinessObject
Teamcenter의 Modeling 에서 가장 최상위 Model.

가장 기본적인 다음 4가지의 Runtime 속성을 지원한다.

| Property Name | Type | Storage Type | Array | Template |
|---|---|---|---|---|
|	awb0SupportsStructure	|	Runtime	|	Boolean	|	:heavy_multiplication_x:	|	activeworkspacebom	|
| awp0CellProperties 		| Runtime	|	String[400] | :heavy_check_mark: | aws2 |
|	awp0ThumbnailImageTicket	|	Runtime	|	String[400]	|	:heavy_multiplication_x:	|	aws2	|
|	awb0SupportsStructure	|	Runtime	|	String[4000]	|	:heavy_multiplication_x:	|	foundation	|