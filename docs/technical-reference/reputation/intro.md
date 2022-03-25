---
sidebar_position: 1
title: Introduction
---

# Reputation

The heart of Interep lies in the possibility to export reputation. However, calculating it is not an easy task, at least as far as social networks are concerned. Some parameters are easier to fake and others do not offer an objective representation of the user's reputation. Our methods try to select the most suitable parameters and calculate a score that falls into one of the following categories (or reputation levels): `gold`, `silver`, `bronze`. Parameters such as `followers`, `likes`, `stars` can then be used to obtain a score that can best represent the authenticity of a user. The following paragraphs describe the criteria used by the social media platforms supported by Interep.

:::tip
If you want to see how we calculate reputation or if you want to integrate our methods into your app, we have a dedicated [`@interep/reputation`](https://github.com/interep-project/interep.js/tree/main/packages/reputation) package.
:::
