---
title: "Adventures with Hugo: Configure Hugo's Native Syntax Highlighting On Micro.Blog"
microblog: false
guid: http://matti.micro.blog/2022/01/08/configure-hugos-native.html
post_id: 1479904
date: 2022-01-08T01:20:00+0200
lastmod: 2022-02-18T09:13:23+0200
type: post
categories:
- "Blog"
images:
- https://cdn.uploads.micro.blog/44388/2022/f32609ded9.png
photos:
photos_with_metadata:
permalink: /2022/01/08/configure-hugos-native.html
---
If you are one of [the brave people](https://www.manton.org/2022/01/07/moving-to-new.html) that uses Hugo Version 0.91 and wants to take advantage of Hugo's [native syntax highlighting](https://gohugo.io/content-management/syntax-highlighting/) capabilities on a light theme (like the default theme in this example), you might be surprised:

![](/media/uploads/2022/f32609ded9.png)

As you can see… you can't really see much.

Thankfully this can be changed, by changing the configuration for syntax highlighting. But in order to do that you have to know the following:

<blockquote class="quoteback" data-title="" data-author="Jason Cardwell" data-avatar="https://micro.blog/Moondeer/avatar.jpg" cite="https://micro.blog/Moondeer/12348161"><p><a href="https://micro.blog/matti">[@matti](https://micro.blog/matti)</a> interesting … so much is still a blackbox for me. I just tinker until I get results. My two favorite finds are the config directory (which take precedent ahead of the json files) and the assets directory (with which you can build Javascript and Sass files from templates).</p>
<footer>Jason Cardwell <cite><a href="https://micro.blog/Moondeer/12348161">https://micro.blog/Moondeer/12348161</a></cite></footer></blockquote><script src="https://micro.blog/quoteback.js"></script>

You have to know about the precedence because for some reason, changing the config.json in your theme won't do the trick. This is how it works:

## Get A Functioning Custom "New-Plugin-Style"-Default-Theme For Your Blog

EDIT 18.02.2022: The following is not up to date anymore. Plugin-Themes now behave much more convenient: Just install the theme, activate for your blog, create a custom theme and only add `config/_default/markup.json` template.

~~First of all make sure you are on the Hugo version 0.91 (dropdown in the Design screen, remember to save) and install the default theme as a plugin (Plug-ins screen). Then go to Design again and click on "Edit Custom Themes", on the next screen click on the default theme and duplicate it with the button in the next screen. You should now be back in the custom themes overview list. Click Design in the sidebar once more and choose your custom theme, save. Click "Edit Custom Themes" again and then on your copy of the Default theme.[^1]~~


## Change Configuration

You should now be inside your custom theme screen. Click on "New Template". You will be presented wie the template editor and theme preview split view.

Name the template `config/_default/markup.json` and set its contents to:

```json
{
    "highlight": {
      "anchorLineNos": false,
      "codeFences": true,
      "guessSyntax": false,
      "hl_Lines": "",
      "lineAnchors": "",
      "lineNoStart": 1,
      "lineNos": true,
      "lineNumbersInTable": true,
      "noClasses": true,
      "style": "monokailight",
      "tabWidth": 4
    }
}
```

This is basically the [default config from the Hugo documentation](https://gohugo.io/getting-started/configuration-markup#highlight), except that for style we use `monokailight` instead of `monokay`. Click "Update Template", your site should be rebuilding as indicated by the spinner. When Hugo is done, syntax highlighting should now be working as intended and the code be legible.

Example:

{% raw %}
```go-html-template
{{ define "main" }}
<div class="home h-feed">
  <ul class="post-list">
  {{ $paginator := .Paginate (where (where .Site.RegularPages.ByDate.Reverse "Type" "post") "Params.title" "!=" nil   ) (index .Site.Params "archive-paginate" | default 25) }}
  {{ range $paginator.Pages  }}
      <li class="h-entry">
			<h1><a href="{{ .Permalink }}">{{ .Title }}</a></h1>

        <a href="{{ .Permalink }}" class="u-url"><span class="post-meta"><time class="dt-published" datetime="{{ .Date.Format "2006-01-02 15:04:05 -0700" }}">{{ .Date.Format "Jan 2, 2006" }}</time></span></a>

        <div class="e-content">
         	{{ .Content }}
        </div>
      </li>
    {{ end }}
  </ul>

  <p class="rss-subscribe">subscribe <a href="{{ "feed.xml" | absURL }}">via RSS</a></p>

</div>
{{ end }}
```
{% endraw %}

~~[^1]: I'm not sure if this is all necessary or even the right way to go about it. It seems pretty involved and I don't even know how you would migrate your customizations in an easy way if you happen to have used the old style of choosing a theme… but this way works, that much I could prove.~~
