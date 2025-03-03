---
title: "How to Fix RSS Feed Location for GitHub Pages"
date: 2025-03-03T17:54:00+01:00
draft: false
---

When using GitHub Pages to host your blog, you might encounter an issue where the RSS feed is not located where you expect it to be. This can be particularly problematic if you want your blog to be syndicated and need the RSS feed to be in a specific location. In this post, I'll walk you through how I resolved this issue for my blog.

## The Problem

I was using GitHub Pages to host my blog at [https://lewispen.github.io/lewiswrites](https://lewispen.github.io/lewiswrites). However, the RSS feed was being looked for at [https://lewispen.github.io/rss.xsl](https://lewispen.github.io/rss.xsl), whereas my RSS file was actually located at [https://lewispen.github.io/lewiswrites/rss.xsl](https://lewispen.github.io/lewiswrites/rss.xsl). This discrepancy was causing issues with syndication.

GitHub Pages was appending the name of my repository (righytly) to the end of my website. I didn't want this though so went to find a solution.

## The Solution

The fix for this issue was to rename the repository to match the desired site name. In my case, I renamed the repository to `lewispen.github.io`. This change made my RSS feed sit in the expected place.

## Steps to Fix the RSS Feed Location

1. **Rename the Repository**: Go to your GitHub repository settings and rename your repository to `lewispen.github.io`.

2. **Update Your GitHub Pages Settings**: Ensure that your GitHub Pages settings are pointing to the correct branch (usually `main` or `gh-pages`).

3. **Verify the RSS Feed Location**: After renaming the repository, your RSS feed should now be located at [https://lewispen.github.io/rss.xsl](https://lewispen.github.io/rss.xsl).

## Example

**Before renaming the repository:**

- Blog URL: [https://lewispen.github.io/lewiswrites](https://lewispen.github.io/lewiswrites)
- RSS Feed URL: [https://lewispen.github.io/lewiswrites/rss.xsl](https://lewispen.github.io/lewiswrites/rss.xsl)

**After renaming the repository:**

- Blog URL: [https://lewispen.github.io](https://lewispen.github.io)
- RSS Feed URL: [https://lewispen.github.io/rss.xsl](https://lewispen.github.io/rss.xsl)

## Conclusion

By renaming the repository to match the desired site name, I was able to resolve the issue with the RSS feed location. This simple change ensured that the RSS feed was in the expected place, allowing for proper syndication of my blog.

I hope this helps anyone facing a similar issue with their GitHub Pages setup!