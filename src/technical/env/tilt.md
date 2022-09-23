# Tilt (Devnet)

### What is Tilt?

[Tilt](https://tilt.dev/) is part of the official Docker ecosystem. It's a tool which allows developers to easily configure a Kubernetes environment for development.

However, in the context of Wormhole, 'Tilt' usually refers to the development environment used by the [Wormhole Core Repository](https://github.com/wormhole-foundation/wormhole). This environment uses Tilt to stand up docker images for all the tools necessary to build across multiple blockchains, including:

- All the Wormhole supported blockchains / ecosystems
- A Guardian Node
- Relayers
- Databases, Redis
- Utility frontends

The 'Tilt' environment (also referred to as Wormhole 'Devnet') is meant to provide an entire cross-chain development stack right out of the box.

### Is Tilt Right for You?

Tilt is generally a good starting point for most developers. Here's a succinct list of the pros and cons of the environment, so you can decide if it's the right fit for you.

### Pros

- Out-of-the-box support for the many components needed to develop across the heterogenous blockchain space.
- Consistent development environment, where contracts deploy deterministically and everything is already linked up.
- Ability to easily enable/disable components as needed.
- Regularly updated as new components join the Wormhole ecosystem.

### Cons

- Relatively high system requirements. This can be mitigated by disabling components.
- Most blockchains are 'fresh' and have no contracts by default. Thus, you may have to deploy your own dependencies, or alter the default tilt configuration.
- Spin-up and rebuild times can be slow. This can result in a slow workflow if you rely on docker rebuilds.

# Setting up Tilt

Tilt functions best in a UNIX-style environment. For Windows users, using a WSL environment is recommended.

In order to run the Tilt environment, you'll first need to make sure you have [Tilt](https://docs.tilt.dev/install.html) and [Go](https://go.dev/doc/install) installed.

Once you've installed these two dependencies, just clone the Wormhole Core Repository and start Tilt.

```
git clone --branch dev.v2 https://github.com/wormhole-foundation/wormhole.git

cd wormhole

tilt up
```

Be sure to check out the [**Tiltfile**](https://github.com/wormhole-foundation/wormhole/blob/dev.v2/Tiltfile), which has much of the configuration and arguments for the development environment. It's relatively straightforward to enable and disable components. For example, you can disable blockchains by setting them to false at startup

```
tilt up -- --algorand=false --near=false --solana=false terra_classic=false terra2=false
```

# Using Tilt

Tilt can pretty much be treated as though it's an external environment that you can easily spin up and tear down.

If you've followed the standard setup, all your resources will be bound to various ports on localhost. To see all the endpoints which are being hosted in your Tilt environment, you should check the Tilt dashboard, located at [http://localhost:10350/overview](http://localhost:10350/overview).

Tilt is alos referred to as 'Devnet' in the Wormhole ecosystem, so anywhere you see information labeled as 'Devnet', you can apply it to Tilt.

For example, you can find all the deployed contract addresses in the 'Devnet' [constants](https://github.com/wormhole-foundation/wormhole/blob/dev.v2/sdk/js/src/utils/consts.ts) of the Wormhole Typescript SDK.

Useful information pertaining to funded wallets & useful private keys can also be found in the [devnet.md](https://github.com/wormhole-foundation/wormhole/blob/dev.v2/docs/devnet.md) file of the docs.

From here, Tilt is quite similar to using Testnet, and you should look at the [Tooling](./tooling.md) page for additional resources.

In order to shut down Tilt, simply run

```
tilt down
```