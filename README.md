# Crypto Hot Store

This hot wallet creates an environment, with customizable checks and balances, that sends cryptocurrency payments to specified addresses.

## How It Works

This utilises two of two (at least -- could be three but more would make it less secure) multisig. The application is meant to run in as separate instances: one as a `maker`, and one as a `checker`.

The `maker`:

- is the instance that receives payment instructions from the app that wants the payment to be made
- has one of private keys used to spend funds
- knows the total balance in the wallet, per cryptocurrency
- notifies the admin when thresholds, which are customizable, are reached (i.e. bitcoin wallet has less than 2 bitcoins)
- notifies the admin if a withdrawal is larger than the amount available in the wallet (i.e. user wants to withdraw 1 bitcoin but only 0.9 is available)
- crafts the transaction and sends it to the `checker`

The `checker`:

- receives a crafted transaction from the `maker`, and signs it based on certain customizable conditions
- can sign automatically if below a rate limited threshold (i.e. withdrawals of less than 1 bitcoin per hour)
- may require manual approval if a threshold is passed
- signs the transaction and broadcasts it to the network when authorizated

We recommend that the `maker` and `checker` modes are run in reasonably separate environments, ideally run by different people. All that is needed for an individual to spend the funds that these apps control are the private keys of the `maker` and `checker`.

## Supported cryptocurrencies

- Bitcoin (currently being worked on)

## Dependencies

- Access to nodes of the blockchains supported, ideally a different one for the `maker` and `checker`

## Deployment

TODO
