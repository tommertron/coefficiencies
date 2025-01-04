+++
date = '2025-01-04T11:26:20.609588-05:00'
draft = false
title = 'Site RSS Update'
+++


I just updated my site to include full-text RSS feeds, as God intended. I’m really not sure why this isn’t enabled by default in Hugo. What’s worse is the default RSS feed only contains a post’s summary, with no “read more…” link so readers might be inclined to think that that’s the whole post.

Anyway, I enabled it by following the [instructions on Jason Murray’s site](https://jasonmurray.org/posts/2021/rssfulltexthugo/), except the linked file that’s required is no longer available on his GitHub page. Luckily, I reached out and he was happy to provide it for me. I’m going to include the full code for it on this page for posterity.

	{{- $pctx := . -}}
	{{- if .IsHome -}}{{ $pctx = .Site }}{{- end -}}
	{{- $pages := slice -}}
	{{- if or $.IsHome $.IsSection -}}
	{{- $pages = $pctx.RegularPages -}}
	{{- else -}}
	{{- $pages = $pctx.Pages -}}
	{{- end -}}
	{{- $limit := .Site.Config.Services.RSS.Limit -}}
	{{- if ge $limit 1 -}}
	{{- $pages = $pages | first $limit -}}
	{{- end -}}
	{{- printf "<?xml version=\"1.0\" encoding=\"utf-8\" standalone=\"yes\"?>" | safeHTML }}
	<rss version="2.0" xmlns:atom="http://www.w3.org/2005/Atom">
	  <channel>
	    <title>{{ if eq  .Title  .Site.Title }}{{ .Site.Title }}{{ else }}{{ with .Title }}{{.}} on {{ end }}{{ .Site.Title }}{{ end }}</title>
	    <link>{{ .Permalink }}</link>
	    <description>Recent content {{ if ne  .Title  .Site.Title }}{{ with .Title }}in {{.}} {{ end }}{{ end }}on {{ .Site.Title }}</description>
	    <generator>Hugo -- gohugo.io</generator>{{ with .Site.LanguageCode }}
	    <language>{{.}}</language>{{end}}{{ with .Site.Author.email }}
	    <managingEditor>{{.}}{{ with $.Site.Author.name }} ({{.}}){{end}}</managingEditor>{{end}}{{ with .Site.Author.email }}
	    <webMaster>{{.}}{{ with $.Site.Author.name }} ({{.}}){{end}}</webMaster>{{end}}{{ with .Site.Copyright }}
	    <copyright>{{.}}</copyright>{{end}}{{ if not .Date.IsZero }}
	    <lastBuildDate>{{ .Date.Format "Mon, 02 Jan 2006 15:04:05 -0700" | safeHTML }}</lastBuildDate>{{ end }}
	    {{- with .OutputFormats.Get "RSS" -}}
	    {{ printf "<atom:link href=%q rel=\"self\" type=%q />" .Permalink .MediaType | safeHTML }}
	    {{- end -}}
	    {{ range $pages }}
	    <item>
	      <title>{{ .Title }}</title>
	      <link>{{ .Permalink }}</link>
	      <pubDate>{{ .Date.Format "Mon, 02 Jan 2006 15:04:05 -0700" | safeHTML }}</pubDate>
	      {{ with .Site.Author.email }}<author>{{.}}{{ with $.Site.Author.name }} ({{.}}){{end}}</author>{{end}}
	      <guid>{{ .Permalink }}</guid>
	      <description>{{ .Content | html }}</description>
	    </item>
	    {{ end }}
	  </channel>
	</rss>

Oh, for good measure, the site now includes an RSS icon/link to the feed in the menu bar. Go RSS!