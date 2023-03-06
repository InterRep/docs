---
sidebar_position: 2
---

# OAuth

Users who have Reddit, Twitter or Github accounts can access Interep with OAuth authentication. Interep will then be able to obtain the parameters needed to calculate their reputation on the platform, and depending on this reputation users will be able to join, and then possibly leave, the related Interep groups.

## Flow

1. The user logins to one of our supported OAuth providers and Interep calculates their reputation on that platform;
2. the user connect their Metamask wallet;
3. the user generates an identity commitment for the OAuth provider;
4. the user joins or leaves the group related to their reputation on the platform where they are authenticated.

![OAuth flow](/img/oauth_flow.svg)

:::caution
Users can only authenticate to one OAuth provider at a time.
:::

## Use cases

### 1. Web3 social networks

Social networks are used on a global scale and play a crucial role in our societies. Since reputation is the primary metric for determining how much and in what way a platform is used, allowing users to easily export their reputation to access external services can drastically limit the number of fake accounts and Sybil attacks. The new generation of decentralized social networks can leverage users' reputation previously earned on other platforms and create a less toxic environment. Users, even the anonymous ones, would in any case correspond to real people.

### 2. Testnet faucets

Testnet faucets allow developers to get ethers to test their DApps and contracts on Testnet networks. Since these services require some form of verification to avoid too many requests from bots or fake accounts, it is quite difficult to get ethers without sharing personal data. A user with a high reputation on Twitter belonging to an Interep group could, for example, prove their authenticity without sharing any data, and thus obtain the ethers he needs for the development of their DApp.

### 3. Allocating funds to public goods

Allocating funds towards public goods efficiently, safely, and fairly is a complex challenge. One of the main problems in this type of context is the uniqueness of the contributors. Interep groups can be used to ensure that each contributor is unique based on membership in one or more groups.

## Available groups

Currently, there are three OAuth providers: Twitter, GitHub and Reddit. For each of them there will be one of the following groups based on the user's reputation level: **`commoner`**, **`up-and-coming`**, **`established`**, **`star`** and **`icon`**.

:::info
If you want to know how Interep calculates reputation click [here](/technical-reference/reputation/intro).
:::
