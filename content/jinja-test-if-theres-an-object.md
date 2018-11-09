---
title: Jinja Test if Theres an Object
image:
imageMeta:
  attribution:
  attributionLink:
featured: true
author: carlos
date: Tue Oct 30 2018 16:29:24 GMT+0000 (GMT)
tags:
  - new
---

# Write Me

in config add to jinja environment variables
    
    app.jinja_env.globals['undefined_check'] = helpers.undefined_check

define it in helpers.py

    def undefined_check(item, item_property):
        if item:
            if item_property in ['start', 'end']:
                prop = getattr(item, item_property)
                return prop.strftime('%m/%Y')
            return getattr(item, item_property)
        else:
            return ''

Use it in template

    <input type="hidden" name ="actionId" value="{{ undefined_check(action_item, 'id') }}">


