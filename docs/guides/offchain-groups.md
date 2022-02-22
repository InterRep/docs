---
title: Offchain groups
---

# Using offchain groups

In this section, we will learn how to integrate our Interep offchain groups in your application.

Interep allows users to join groups anonymously, so that these groups can then be used by DApps and external services to allow, for example, only certain categories of users to authenticate or to unlock certain features based on the user's group. Each group has a certain provider and a name (which coincides with the reputation when there is a OAuth provider). A user with a gold reputation on Twitter can, for example, join the relevant group and access another application by proving that they are part of the group and therefore have a gold reputation.

The groups are basically composed of a set of Semaphore identity commitments organized in Merkle trees. Thanks to Semaphore it is possible to create a zero-knowledge proof to prove that a user is a member of the group (or a leaf of the tree) without revealing their identity.

In the following steps we will use [`@interep/api`](https://github.com/Interep/interep.js/tree/main/packages/api), a JavaScript library to wrap our REST APIs. If you want to use our API directly, you can find them in the [API](/api) section.

:::caution
Before going any further, if you are not familiar with Semaphore, read the [official documentation](https://semaphore.appliedzkp.org).
:::

:::info
If you want to integrate the whole onboarding flow into your UI, follow all the steps. Otherwise, if you want to redirect the user to our app to allow him/her to join a group, follow the steps in the following order: 3, 5, 6. Just remember that for Email and Telegram providers you can't use the API to add and remove id commitment in groups.
:::

## 1. Generate a OAuth token

If you want to allow a user to join a group directly from your app without going through the Interep app, you will need to create a OAuth authentication system to generate a valid access token in order to calculate the users' reputation and to add their identity commitment to a Interep group. You can get the list of our supported providers with our [`@interep/api`](https://github.com/Interep/interep.js/tree/main/packages/api) package.

```typescript
import { API } from "@interep/api"

const api = new API()
const providers = await api.getProviders()

console.log(providers) // ["twitter", "github", "reddit", "poap", "telegram", "email"]
```

:::info
You only need to create a token if the provider is a OAuth provider (e.g. Twitter, Reddit, Github). For the Web3 providers (e.g POAP) you can skip the steps 1 and 2. As we will see later, it is sufficient to sign the identity commitment with Metamask and send the signature and the address of the Ethereum account used to sign.
:::

## 2. Calculate the user's reputation

Once you have generated a valid OAuth token and are able to obtain the user's account data you can calculate their reputation with our [`@interep/reputation`](https://github.com/Interep/interep.js/tree/main/packages/reputation) package.

```typescript
import { calculateReputation, OAuthProvider } from "@interep/reputation"

// 'getGithubUserByToken' is an example function.
const { id, plan, followers, receivedStars } = await getGithubUserByToken(token)

const reputation = calculateReputation(OAuthProvider.GITHUB, {
    proPlan: plan.name === "pro",
    followers,
    receivedStars
})

console.log(reputation) // gold
```

## 3. Create the identity commitment

Creating an Semaphore identity commitment is quite simple. Interep provides an [`@interep/identity`](https://github.com/Interep/interep.js/tree/main/packages/identity) package to create a Semaphore identity ([`@libsem/identity`](https://github.com/appliedzkp/libsemaphore/tree/master/packages/identity)). You will also need [Metamask](https://metamask.io/) and [Ethers.js](https://github.com/ethers-io/ethers.js/) (or [Web3.js](https://github.com/ChainSafe/web3.js)) to sign the Interep message. If you want to see how `@interep/identity` works you can try our [demo](https://js.interep.link/identity/).

```typescript
import createIdentity from "@interep/identity"
import detectEthereumProvider from "@metamask/detect-provider"
import { ethers } from "ethers"

const ethereumProvider = await detectEthereumProvider()
const provider = new ethers.providers.Web3Provider(ethereumProvider)
const signer = provider.getSigner()

function sign(message: string): Promise<string> {
    return signer.signMessage(message)
}

const identity = await createIdentity(sign, "github")
const identityCommitment = identity.genIdentityCommitment().toString()
```

## 4. Add the identity commitment to a group

To add an identity commitment to a group you need a OAuth token if there is a OAuth provider or the signature of the identity commitment and the Ethereum account address if there is a Web3 provider.

The POST methods of our APIs are restricted to a list of domains defined in a whitelist. If you want to add your own domain please contact us or open a pull request. You can find the configuration file [here](https://github.com/Interep/reputation-service/blob/main/src/config.ts).

```typescript title="Adding identity commitments to groups with reputation providers (e.g Github)."
await api.addIdentityCommitment({
    provider: "github",
    name: reputation,
    identityCommitment,
    authenticationHeader: `token ${token}`
})
```

```typescript title="Adding identity commitments to groups with Web3 providers (e.g POAP)."
import detectEthereumProvider from "@metamask/detect-provider"
import { ethers } from "ethers"

const ethereumProvider = await detectEthereumProvider()
const provider = new ethers.providers.Web3Provider(ethereumProvider)
const signer = provider.getSigner()

const userSignature = await signer.signMessage(identityCommitment)
const userAddress = await signer.getAddress()

await api.addIdentityCommitment({
    provider: "poap",
    name: "devcon4",
    identityCommitment,
    userAddress,
    userSignature
})
```

:::info
If you need to get our supported groups you can use the `api.getGroups()` function.
:::

## 5. Get the Merkle tree proof

After the user is part of a group, you can obtain the Merkle tree proof needed to generate the proof of membership with Semaphore.

```typescript
const proof = await api.getMerkleTreeProof({
    provider: "github",
    name: reputation,
    identityCommitment
})
```

## 6. Create a zero-knowledge proof

At this point you have all the necessary parameters to generate a zero-knowledge proof with Semaphore.
