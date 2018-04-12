---
layout: page
title: "Installing third-party add-ons"
description: "Instructions on how to get started using third-party add-ons."
date: 2017-05-14 13:28
sidebar: true
comments: false
sharing: true
footer: true
---

Hass.io allows anyone to create add-on repositories to share their add-ons for Hass.io easily. To try this locally, you can use our example add-on repository at

```text
https://github.com/home-assistant/hassio-addons-example
```

<p class='note warning'>
Home Assistant cannot guarantee the quality or security of third-party add-ons. Use at your own risk.
</p>

<p class='img'>
<img src='/images/hassio/screenshots/main_panel_addon_store.png' />
From the Hass.io main panel open the add-on store.
</p>

<p class='img'>
<img src='/images/hassio/screenshots/adding_repositories.png' />
Add the URL of the repository and then press "Add". A new card for the repository will appear.
</p>

### {% linkable_title Help: Repository is not showing up %}

If you have added a repository, but it's not showing up, it means that the repository contains invalid configuration. Go to the Hass.io panel and then the System tab to find the System log. It should tell you what went wrong. Report this information to the repository author.
