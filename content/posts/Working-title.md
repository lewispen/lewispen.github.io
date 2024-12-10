---
title: "Working Hugo issue title"
date: 2024-12-09T17:35:11+01:00
draft: true
---

I was having an issue getting getting my blogs RSS feed for syndication at work.

My site was looking at the base url, but GitHub was appending my repo name onto the end of my url, meaning that the rss.xsl was looking at {sitename{/lewiswrites}.rss.xsl rather than just sitename.rss.xsl.

To avoid this issue, make sure that the repo is named the same as the site in GitHub. So name your repository site.github.io, this gives your website the same name as the repo.