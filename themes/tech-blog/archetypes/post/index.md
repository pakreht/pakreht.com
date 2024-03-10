{{- $title := replace .Name "-" " " | title -}}
{{- $dir := path.Clean .File.Dir -}}
{{- $category := index (split $dir "/") 1 -}}
{{- $taxonomy := printf "%s/tags" $category -}}
{{- $terms := slice -}}
{{- range $k, $v := (index .Site.Taxonomies $taxonomy) -}}
    {{- $terms = $terms | append $k -}}
{{- end -}}
---
title: {{ $title }}
category: {{ $category }}
date: {{ now.Format "2006-01-02" }}
# description = "Optionnal SEO Description"
{{- $termsInQuote := apply $terms "printf" "'%s'" "." }}
{{ $taxonomy }}: [{{delimit $termsInQuote ", "}}]
---

This is a post in category **{{ $category }}** about **{{ $title }}**.