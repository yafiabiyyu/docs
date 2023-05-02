---
title: Creating Secure ERC721 Contracts Made Easy with Vyper and Celo Randomness
description: This tutorial is designed to make creating an ERC721 contract using Vyper programming language more convenient for you. With the ability to Random mint using Celo Randomness
authors:
  - name: Abiyyu Yafi
    title: Python Developer
    url: https://github.com/yafiabiyyu
    image_url: https://github.com/yafiabiyyu.png
tags: ["celosage", "intermediate", "erc721", "randomness"]
hide_table_of_contents: true
slug: /tutorials/creating-secure-erc721-conracts-made-easy-with-vyper-and-celo-randomness
---

![header](../../src/data-tutorials/showcase/intermediate/creating-secure-erc721-conracts-made-easy-with-vyper-and-celo-randomness.png)


## Introduction

Vyper, an open-source programming language created specifically for building smart contracts on the Ethereum blockchain. Vyper aims to make it easier for developers to create smart contracts that are more secure and auditable. It is based on Python but has a simpler syntax and supports only a limited number of potentially risky Python features, such as dynamic typing, inheritance, and operator overloading. Vyper's main advantage is its focus on security, with features like strong typing, integer overflow protection, and gas cost estimation designed to prevent mistakes in smart contract development. Additionally, Vyper supports the ERC20, ERC721, and ERC777 smart contract standards. While still under active development, Vyper has gained popularity as a choice for developers seeking to build more secure and auditable smart contracts on the Ethereum blockchain.


## Prerequisites

Before starting the tutorial *Creating Secure ERC721 Contracts Made Easy with Vyper and Celo Randomness* make sure you meet the following prerequisites:

1. Have basic knowledge of blockchain and smart contracts.
2. Have experience using the terminal (command-line interface) on the operating system you are using.
3. Have knowledge of the Python programming language and a basic understanding of its syntax and code structure.
4. Have a registered Celo account on the Alfajores network with a balance to pay transaction fees.
5. Have an understanding of standard ERC721 smart contracts and how they are used to create unique assets.

Meeting these requirements is essential for proper understanding and optimal results.


## Requirements

- [Python3](https://www.python.org/downloads/release/python-368/) or greater
- [NodeJs](https://nodejs.org/en/) >= v14.0.0 and npm >= 6.12.0 (For Ganache)
- [Ganache](https://www.trufflesuite.com/ganache) (For local blockchain)
- [eth-brownie](https://eth-brownie.readthedocs.io/en/stable/install.html) (For development and testing smart contracts)
- [python-dotenv](https://pypi.org/project/python-dotenv/) (For loading environment variables from .env file)


This is a list of what we’ll cover 🗒

- ✅ **Step 1:** Project setup
- ✅ **Step 2:** Write project code
- ✅ **Step 3:** Configure deployment settings
- ✅ **Step 4:** Deploy your Contract
- ✅ **Step 5:** Integration with frontend


## **Step 1:** Project setup

let's create a new directory by running the following command in your terminal, and navigate into the project directory.

```bash
mkdir vyper-erc721 && cd vyper-erc721
```

Now, we need to install the required packages. This will install all the dependencies needed to run our project.

```bash
# install eth-brownie and python-dotenv
pip3 install eth-brownie python-dotenv

# install ganache
npm install -g ganache
```

To start the project, we need to initialize it using brownie. Open your terminal and enter the following command to initialize the project

```bash
brownie init
```

If successful, you will see output like this

![Initialize Project](image/1.png)

To integrate Celo Network into Brownie, you must run a command in your terminal. This command will add Celo Network to Brownie and enable you to develop and test smart contracts on the Celo blockchain

```bash
# Celo Mainnet
brownie networks add Celo celo-mainnet host=https://forno.celo.org chainid=42220 explorer=https://explorer.celo.org

# Celo Alfajores Testnet
brownie networks add Celo celo-alfajores host=https://alfajores-forno.celo-testnet.org chainid=44787 explorer=https://alfajores-blockscout.celo-testnet.org
```

After successfully adding the Celo network to Brownie, you can view the list of added networks by running the following command in your terminal

```bash
brownie networks list
```

Next, in our project directory, we need to create two new files: .env and brownie-config.yaml. The .env file stores the environment variables that we'll use, while the brownie-config.yaml file stores the brownie configuration.

```yaml
# brownie-config.yaml
project_structure:
    build: build
    contracts: contracts
    interfaces: interfaces
    reports: reports
    scripts: scripts
    tests: tests
compiler:
    vyper:
        version: 0.3.7
networks:
    default: celo-alfajores
console:
    show_colors: true
    color_style: monokai
    auto_suggest: true
    completions: true
    editing_mode: emacs
dotenv: .env
wallets:
    from_mnemonic: ${MNEMONIC}
```

```yaml
# .env
MNEMONIC="<YOUR_MNEMONIC>"
```