---
title: 'Projects'
showAuthor: false
showDate: false
showTaxonomies: false
showReadingTime: false
showWordCount: false
showComments: false
showSummary: false
showViews: false
showPagination: false
showLikes: false
sharingLinks: false
showRelatedContent: false
layoutBackgroundHeaderSpace: false
---

## Shaders Vault

{{< video 
    src="shaders_showreel.mp4"
    caption="Some of the effects you will find in shaders vault."
    autoplay="true"
    loop="true"
    muted="true"
    controls="false"
    playsinline="true"
>}}

---

I originally started working with shaders during my undergraduate dissertation, and have since fallen in love with them. I enjoy spending my free time tinkering with new effects and bringing ideas to life.

Shaders Vault is a collection of shaders I've worked on, spanning focused techniques like stencil shaders to fully realized effects, including my remake of the portal from Spyro: Reignited Trilogy.

{{< button href="https://github.com/danielpokladek-shaders" >}}
See on GitHub!
{{< /button >}}

## PixiJS Particle System

{{< video 
    src="pixi-particle-system-showcase.mp4"
    caption="PixiJS Particle System with it's companion web-based editor."
    autoplay="true"
    loop="true"
    muted="true"
    controls="false"
    playsinline="true"
>}}

{{< github repo="danielpokladek/pixi-particle-system" showThumbnail=false >}}

---

A modern, flexible particle system for PixiJS - a spiritual successor to the original particle emitter, but rebuilt with a clean TypeScript-first architecture and more expressive API.

I originally started working on this project alongside a PixiJS-based portfolio project, where I needed a particle system for several in-game effects. At the time, the original emitter package wasn't compatible with the latest PixiJS version.

As the library grew and I introduced more personal improvements, it evolved beyond it's original scope. I eventually decided to make it open-source and share it with the wider community.

## Website

{{< figure
    src = "website_banner.webp"
    nozoom = true
>}}

{{< github repo="danielpokladek/blog" showThumbnail=false >}}

---

Oh look, you're here!

This website is built using the [Hugo](https://github.com/gohugoio/hugo) static site framework with the [Blowfish](https://github.com/gohugoio/hugo) theme, customized to suit my needs. I chose a static-site approach for its performance, simplicity, maintainability, and blogging integration.

The site is hosted on GitHub Pages, with GitHub Actions handling automated builds and deployment. Every change is built and deployed through a lightweight CI pipeline, keeping the workflow fast, repeatable, and hands-off.