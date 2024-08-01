---
title: "Oh-my-posh Configuration File"
date: "2024-08-01"
categories: ["cli"]
---

```json
{
    "version": 2,
	"$schema": "https://raw.githubusercontent.com/JanDeDobbeleer/oh-my-posh/main/themes/schema.json",
    "final_space": true,
    "auto_upgrade": true,
    "disable_notice": true,
    "transient_prompt": {
        "background": "#363039",
        "foreground": "#F3AF31",
        "template": "<#363039,transparent>\ue0b6</><#F3AF31,#363039>{{.Folder}} </>\u276f<#363039,transparent>\ue0b4 </>",
        "type": "text"
    },

	"blocks": [
        {
			"alignment": "left",
			"segments": [
				{
					"background": "#F3AF31",
					"foreground": "#363039",
					"leading_diamond": "\ue0b6",
					"style": "diamond",
					"template": "{{ .Folder }} \u276f",
					"trailing_diamond": "\ue0b4",
					"type": "text"
				}
			],
			"type": "prompt"
		},
		{
			"alignment": "right",
			"segments": [
				{
					"background": "#F3AF31",
					"foreground": "#363039",
					"foreground_templates": [
						"{{ if or (.Working.Changed) (.Staging.Changed) }}#363039{{ end }}",
						"{{ if and (gt .Ahead 0) (gt .Behind 0) }}#363039{{ end }}",
						"{{ if gt .Ahead 0 }}#B388FF{{ end }}",
						"{{ if gt .Behind 0 }}#B388FF{{ end }}"
					],
					"leading_diamond": " \ue0b6",
					"properties": {
						"branch_max_length": 25,
						"fetch_stash_count": true,
						"fetch_status": true,
						"fetch_upstream_icon": true
					},
					"style": "diamond",
					"template": " {{ .UpstreamIcon }}{{ .HEAD }}{{if .BranchStatus }} {{ .BranchStatus }}{{ end }}{{ if .Working.Changed }} \uf044 {{ .Working.String }}{{ end }}{{ if and (.Working.Changed) (.Staging.Changed) }} |{{ end }}{{ if .Staging.Changed }} \uf046 {{ .Staging.String }}{{ end }}{{ if gt .StashCount 0 }} \ueb4b {{ .StashCount }}{{ end }} ",
					"trailing_diamond": "\ue0b4",
					"type": "git"
				}
			],
			"type": "rprompt"
		}
	]
}
```