﻿    AIP: 1
      Title: Dapp Registry
      Status: Draft
      Type: Meta
      Author: @Vladiuz1 (vlad@array.io)
      Created: 2018-06-13

What is Dapp Registry?
--------------

Dapp registry is a registrar of dapp bundles published or unpublished.

Rationale
---------

A Dapp needs 3 fundamental features:

1. Author verificiation
2. A unique name
3. Versioning system
4. A place with a list of all dapps

The Dapp registry will take care of these tasks.

Description
-----------

The Dapp registry will be implemented by a smartcoctract within Array.io core blockchain.

This smart contract will be responsible for registering new dapp names, with reference to dapp determenistic hash. Both the hash and the name will be used by Array.io-client as keys for referencing an installed app.

The regitry smart contract will make sure that the name is unique. And will also contain the default language of the name. It will also assign an author during registration of the name of a dapp. The author will be identified by account (or address) that has submited name registration request. The author can theoretically be a smart contract.. A multisig for example.

Versioning is another feature of the smart contract. Every new version will be submited to the smart contract, identifying the author (account or address) making sure he has authority over the app, and the registry will assign a new address of the dapp.

Execution of registered and unregistered apps may be allowed/forbidden on the client settings level. If user of client application allows execution of unregistered apps, he will get a warning trying to execute such application, yet it will let her/him execute it. Similar to how osx manages its securities policies regarding what code is allowed to be executed.

Registry must also have transfer ownership functionality.

A smart contract is the easiest way to manage such registry for a few reasons.

Definitions
-----------

*Author* - an entity/person that created the dapp, and registered its name within Dapp Registry smart contract. Author is identified by the account that has current author rights.

*Hash* - deterministic hash based on dapp bundle content. Based on IPFS. Also used to identify a version of the dapp. It is also part of IPFS address if the dapp is published on the network.

*Name* - user friendly name of the dapp.

*Version* - a userfriendly version of the dapp described here: https://github.com/arrayio/array-io-client/issues/14. Every version has its own address in the IPFS (hash).


Functionality
-------------

### Registering a name.

Our dapp names will be part of URI addresses used to reference a dapp or an anchor within a dapp. Hence the dapp names must be unique. In order to provide such uniqness, we must devise a system how to assign a unque name to a dapp. Just like with domains, we anticipate that there may be demand for good application names, and many users may wish to compete for a good dapp name. Proposed smart contract functionality allows for charging a fee for registering a name. This solves a problem of mass registering the names.

Even a small fee will ensure that there is a way to limit the amount of pre-registered names.

Every dapp name must be a ERC721 token, ownership of which can be passed over to other authors. Early registrators of the names, will obviously have edge, but they also risk to loose their investment, and there will be registration fee.

Since registering a name may be done in a decentralized way, we need to make sure that nodes that propagate registration request do no hijack registration and register a good name just before an author trying to register a name or merely looks up a name for uniqueness in a smart contract.

This is achieved by pre-registration. This is how i propose it shall work:

1. think of unique name that has never been used before.