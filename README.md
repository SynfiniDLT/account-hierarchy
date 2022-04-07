# Account Hierarchy

    Copyright (c) 2022, ASX Operations Pty Ltd. All rights reserved.
    SPDX-License-Identifier: Apache-2.0

## Introduction

Custodial services are commonly used throughout the financial services industry. Investors entrust a
custodian with their assets for safekeeping, arrangement of transaction settlement, and management of regulatory and
tax requirements. Being an industry with a long history, custodial services are often built on legacy systems.
A further complexity is that a custodian may also make use of sub-custodians for management of certain assets.
Custodians use separate back office systems, adding the burden of reconciliation between organisations. This
poses a significant risk for custodians when transactions are performed across different custodians or sub-custodians.
Another consequence is the difficulty for custodians to adapt their legacy systems to offer services in new asset
classes, such as cryptocurrencies and digitial assets.

Distributed Ledger Technology (DLT) and the Digital Asset Modelling Language [Daml] (https://daml.com) offer a solution
to the problems posed by existing legacy custodian infrastructure. By storing a register of legal and beneficial
ownership on a distributed ledger, a single source of truth can be made available to custodians, eliminating the need
for reconciliation. Daml as a smart contract language can run on the ledger to enforce the rights and obligations of
custodians and beneficial owners. Unique to Daml is its ability to control the privacy of information at a granular
level which is vital to preserving the privacy of custodians and their customers.

## Project objectives

This project is showcase of research and development carried out by the
[Synfini](https://www2.asx.com.au/connectivity-and-data/dlt-as-a-service) team. It provides a a generic Daml
library to model a register of assets, enabling multi-party workflows between custodians. It extends the existing
[FinLib](https://github.com/digital-asset/lib-finance) library to support multi-level account hierarchies. The core
Daml model currently contains the following components:

- Relationships between custodians/benefciaries and encoding of the account hierarchy tree (
`Synfini.AccountHierarchy.Service` module)
- Allocation of assets to beneficiaries in the hieararchy (`Synfini.AccountHierarchy.Allocation` module)
- Asset transfers and Delivery versus Payment transactions (`Synfini.AccountHierarchy.Trade` module)

In addition, the triggers project contains the following:
- Automated processing of allocation changes to beneficiaries (`Synfini.Trigger.AccountHierarchy.Allocation` module)

## How to use this project

Please note: DAML SDK 1.17.1 must be installed prior to running the following steps.

Firstly, build FinLib, which is a dependency of this project:

```
daml build --project-root lib-finance/model
```

Then build the core models:

```
daml build --project-root core
```

There is also a triggers module which can be used for automation of workflows, which can be built using:

```
daml build --project-root trigger
```

## Documentation

Please use the [example code](examples/src/Synfini/AccountHierarchy/Examples.daml) to understand the structure of the
Daml model and how to use the templates. For each example, there is an accompanying diagram found
[here](examples/diagrams). The public APIs are documented using doc-comments in the Daml source code.
