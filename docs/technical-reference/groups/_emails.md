---
sidebar_position: 4
---

# Emails

Users can join Interep groups that link to certain email domains or certain top level domains. An email address can qualify for zero, one or, at most, two groups, depending on the domains that are available through Interep.

## Flow

1. The user enters their email address on the frontend which is then checked to see if it qualifies the user for any of our groups;
2. if the users email address qualifies they are sent an email containing a magic link;
3. the user clicks on the magic link and is redirected to an appropriate Interep endpoint;
4. the user connect their Metamask wallet;
5. the user selects which group they would like to join (only groups that are eligible to join are shown) and generates an identity commitment for the email provider;
6. the user joins the Interep group or leaves it if they have previously joined.

![Email flow](/img/email_flow.svg)

:::info
If the user has qualified for more than one group then they can join/leave the other group from the same page the magic link sent them to.
:::

## Use cases

### 1. Whistle blowing

You might want to allow individuals to claim that the company they work for has done something illegal but without having to reveal who they are (at least initially). While our system would only be part of a potential process for doing this it would allow an employee, through attesting that they belong to a specific Interep group, to be able to verify that they worked at a specific company and in such a way that the company could not tell which employee was doing this.

There are some caveats to this:

-   To be most effective we would want the identity commitments to need to be recreated periodically to avoid someone being able to pretend that they are still affiliated with a company after they have left.
-   The obfuscation the Interep group provides, while cryptographically secure, has other weaknesses. For example, if only two people at a company have joined the group then while the company might not know which individual one was the whistle blower they could know it was one of the two.
-   To be most effective this would require the employee to get their magic link from their work email, necessarily, but then use it on a computer they had a personal wallet on that would not be monitored by their company.

### 2. Academic groups

You could have a group that only allows people with a .edu address to gain access to it. This could form the basis of an anonymous system of wallets that are controlled by people affiliated with academic institutions. This could then be used as a gateway for certain kinds of on-chain peer review or grant mechanisms that other groups are currently working on.

### 3. Gated groups

While we do not currently support any groups like this, it would be feasible for us to include a pre-set group of email addresses that want to be able to engage in some anonymous activity together, be it voting or otherwise. This flow would then allow all individuals to join an Interep group easily, which is currently not something that users can arbitrarily construct with ease.

## Available groups

Currently we support the following email groups: **`outlook`**, **`hotmail`**, **`.edu`**.

:::caution
The Outlook and Hotmail groups are for testing purposes only allowing people to experience the flow. As they are easy to create many copies of they hold little use in actual applications and will be discontinued in the near future.
:::

:::tip
If you have a domain you would like us to consider adding please get in touch.
:::
