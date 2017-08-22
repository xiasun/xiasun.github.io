---
title: Hexo Asset Folders Tricks
date: 2016-10-29 15:17:24
tags: [hexo, tricks]
---
Hexo provides an individual `asset folder` for each post. Users can use asset method to access those resources in `asset folders` easily. The procedures for using asset folder is described in official [documentation](https://hexo.io/docs/asset-folders.html).

However, the asset method does not support those properties like `width` and `height`, so I would like to recommend using raw `img` tag with a complete path to get resources in asset folders.

The two methods listed below are exactly the same, but the `img` tag could provide more properties:
```
{% asset_img sample.jpg Chrome proxy configuration %}
```

```
<img src="2016/09/21/name-of-post/sample.jpg" width="75%" height="75%" alt="Firefox proxy configuration" title="Firefox proxy configuration">
```
