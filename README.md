# Hedera™ Proof-of-Action Demo / Pasteboard

![](https://img.shields.io/badge/maintenance-as--is-yellow)

Showcases Proof-of-Action (PoA) using the Hedera™ Consensus Service (HCS). 

The general idea is a party can submit an image to the service (and they are given back an identifier). 
On a later date, someone else can submit the same image (or the identifier) and receive "proof" (proof being the 
consensus that was reached for the action of the image submission) of the original
submission and it's related metadata.

## Requirements

* Node.js v12+

* Yarn
 
* [Hedera™ Proof-of-Action API](https://github.com/hashgraph/hedera-proof-of-action-api) - this app is hard-coded to 
  try and talk to the proof-of-action API at `localhost:8080`.

## Setup

* Install dependencies

  ```
  $ yarn
  ```

* Run

  ```
  $ yarn serve
  ```

## License Information

Licensed under Apache License,
Version 2.0 – see [LICENSE](LICENSE) in this repo
or [apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0).
