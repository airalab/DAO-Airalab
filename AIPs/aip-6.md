<pre>
  Title: Add ENS
  Author: Alexander Krupenkin <akru@aira.life>
  Status: implemented
</pre>

# Robonomics ENS
Domain Name System for Robonomics platform
The Robonomics network actively uses the Ethereum Name System in its work, avoiding the explicit use of Ethereum and IPFS addresses.

## Hierarchy of Robonomics Names
Root domain: robonomics.eth

- xrt: Protocol token of the network.
- factory: Factory of liability contracts.
- ambix: Distillation cube (see Evolution of the network).
- *.lighthouse: Lighthouses’ contracts.
- *.validator: Observing networks’ contracts.
- *.model: Foundation agent’s behavioral models.

## Robonomics Network Evolution

Updating of the autonomous processes constitutes a huge problem with contemporary business systems based on a chain of blocks. Currently no integrated solution to this problem has been found. We propose the following solution, based on the evolution of the token, as part of the Robonomics network.

## Network’s version
Let us introduce the concept of a generation or version of the Robonomics network: we will define it as an integer N. We will insert the network’s version into the most basic level in the hierarchy system of the Robonomics names: for example, for the XRT contract of version 3, we will assign the name xrt.3.robonomics.eth. This way, the formation of the Robonomics network’s names will be tied to the version of the network as follows:

{Subdomain}.{Version}.robonomics.eth


## Network update
All Robonomics software addresses the necessary contracts in the current working network domain, including user-assigned contracts, for example, xrt or sensors-network.lighthouse. The working domain is set in the software by default according to the version of the network used, for example, 3.robonomics.eth. In this case, during work, addresses of types like xrt.3.robonomics.eth or sensors-network.lighthouse.3.robonomics.eth are used.

What happens as a result of Robonomics network update. The network version is updated to the latest one, which means that the current working domain is changed in the entire software and while updating the software, a new set of smart contracts existing at the addresses xrt.4.robonomics.eth or sensors-network.lighthouse.4.robonomics.eth will be automatically used. In this case, without updating the user can continue to use the old version of the network.

## Evolution of token
We are talking about evolution as a smooth substitution of one tool by another. In the terms of blockchain, this is similar to a hardfork, since the user can not simultaneously use competing tools. However, there may be multiple groups of users who would use different versions of the same tool on the network.

A suitable tool for making an evolutionary transition is the ambix contract, which allows you to atomically exchange one ERC20 token to another one, equivalent to it. This way, we can implement migration of users from one version of the token to another.

Let there be a smart contract ambix in every working domain of Robonomics and the owner of XRT token, such that the following rule is secured:

xrt.N.robonomix.eth = xrt.(N+1).robonomics.eth
Then the migration of users to (N+1) version will happen according to this scenario:

1. The software that uses the new working domain for the version (N + 1) is updated;
2. Migration script ensuring the following actions is implemented:
2.1. Checks balance of xrt.N.robonomics.eth;
2.2. If balance is above 0, then it sends the transaction to ambix.(N+1).robonomics.eth for distillation.

This way, the migration of autonomous agents to a new version of autonomous processes can be fully automated and would not need any direct human involvement.

## Exchanges as the network participants
Since the digital exchanges, as providers of token exchange for end users, are also members of the network (holders), then they are also given a choice: to continue using the old version of the token or to migrate to the new version. If their choice is determined exclusively by economic considerations, then they will naturally chose the version with the highest turnover of the token. This leads to the following scenario of XRT versions listing on the digital exchanges, which is curiously enough, corresponding with the pipeline of software development:

1. token of (N + 1) version appears — beta release, the number of users is minimal, the turnover is minimal, the digital exchanges are not interested in listing a new token;
2. lighthouses interested in the increased emission of the new version (N + 1) start value migration to a new version of the token with the use of a new infrastructure of smart contracts and software;
3. users interested in the new software features and services provided by lighthouses begin to migrate to the (N + 1) version and start value migration to a new version of the token;
4. exchanges observe the outflow of capital from the N version of token to the (N + 1) version of token, gradually start adding it to the listing, or replacing the existing release token;
5. the remaining participants of N version, witnessing the majority transition to the new version and listing the token on the exchange, complete the transition of the entire network to the (N + 1) version.

## Conclusion
The problem of smart contracts upgrades will arise again and again, and our approach is flexible as it provides the freedom of choice. But it is far from being ideal and a lot of work needs to be done in the future.
