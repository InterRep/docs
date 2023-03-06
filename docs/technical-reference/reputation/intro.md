---
sidebar_position: 1
title: Introduction
---

# Reputation

The heart of Interep lies in the possibility to export reputation.
However, calculating reputation is not an easy task, at least as far as social networks are concerned.
Some parameters are easier to fake and others do not offer an objective representation of the user's reputation.
Based on [analysis of public data](https://github.com/interep-project/interep-groups-eda) collected from each reputation network (github, reddit, twitter) we tried to select and combine parameters that both reflect user's authenticity and result in reputation levels of decreasing sizes.
We defined the following reputation levels: `commoner`, `up-and-coming`, `established`, `star` and `icon`.
The following paragraphs describe the criteria used for each of the social media platforms supported by Interep.

:::tip
If you want to see how we calculate reputation more in details or if you want to integrate our methods into your application, we have a dedicated [`@interep/reputation`](https://github.com/interep-project/interep.js/tree/main/packages/reputation) package.
:::
