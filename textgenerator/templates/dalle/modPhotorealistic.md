---
promptId: 'modPhotorealistic'
name: '🖼️ Generate a Photorealistic photo'
description: 'This will make the art have a lot of detail, but still be stylized, and it will still be art. Do NOT use this if you want to create a prompt which looks like a real photo, as the term “photorealistic” is used to describe an artificial image that looks real, not a real photo.'
author: 'Prompt Engineering Guide'
tags: 'photo, dalle-2, modifier'
version: 0.0.1
stream: false
disableProvider: true
---
```handlebars
{{#run "getPhoto" "r" "tg_selection"}}
 {{selection}}, Photorealistic
{{/run}}
```
***
***
{{get "r"}}