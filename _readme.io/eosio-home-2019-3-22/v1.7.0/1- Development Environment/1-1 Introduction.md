---
title: "1.1 Introduction"
excerpt: ""
---
[block:callout]
{
  "type": "warning",
  "body": "The Docker image is no longer maintained has been deprecated. The `eosio/eos` image from Dockerhub will be available until its sunset on June 29 2018"
}
[/block]

[block:callout]
{
  "type": "info",
  "body": "Looking for the version of this series that uses [Binaries](https://developers.eos.io/eosio-home/docs)?"
}
[/block]

[block:api-header]
{
  "title": "What you'll learn"
}
[/block]
_Only a sample of what you'll learn_
- How to quickly spin up a node
- Manage wallets and keys
- Create Accounts
- Write some contracts
- Compilation and ABI 
- Deploy contracts
[block:api-header]
{
  "title": "EOSIO versions"
}
[/block]
These guides expect you to be using the following (or greater) versions of EOSIO. 

| Component | Version |
| ------ | ------ | 
| dockerhub:eosio/eos | v1.4.2 |
| eosio.cdt | 1.4.1 |
| eosio.contracts | 1.4.0 |
[block:api-header]
{
  "title": "C / C++ Experience"
}
[/block]
EOSIO based blockchains execute user-generated applications and code using WebAssembly (WASM). WASM is an emerging web standard with widespread support of Google, Microsoft, Apple, and industry leading companies. 

At the moment the most mature toolchain for building applications that compile to WASM is clang/llvm with their C/C++ compiler. For best compatibility, it is recommended that you use the EOSIO C++ toolchain.

Other toolchains in development by 3rd parties include: Rust, Python, and Solidity. While these other languages may appear simpler, their performance will likely impact the scale of application you can build. We expect that C++ will be the best language for developing high-performance and secure smart contracts and plan to use C++ for the foreseeable future.

# Linux / Mac OS Experience

The EOSIO software supports the following environments:

* Amazon 2017.09 and higher
* Centos 7
* Fedora 25 and higher (Fedora 27 recommended)
* Mint 18
* Ubuntu 16.04 (Ubuntu 16.10 recommended)
* Ubuntu 18.04
* MacOS Darwin 10.12 and higher (MacOS 10.13.x recommended)
[block:api-header]
{
  "title": "Command Line Knowledge"
}
[/block]
There are a variety of tools provided along with EOSIO which requires you to have basic command line knowledge in order to interact with.
[block:api-header]
{
  "title": "C++ Environment Setup"
}
[/block]
We can use any text editor that, preferably, supports C++ syntax highlighting. Some of the popular editors are Sublime Text and Atom. Another option is an IDE, which provides a more sophisticated code completion and more complete development experience. You are welcome to use the software of your personal preference, but if you're unsure what to use we've provided some options for you to explore. 
[block:api-header]
{
  "title": "Potential Editors and IDEs"
}
[/block]
- [Sublime Text](https://www.sublimetext.com/)
- [Atom Editor](https://atom.io/)
- [CLion](https://www.jetbrains.com/clion/)
- [Eclipse](http://www.eclipse.org/downloads/packages/release/oxygen/1a/eclipse-ide-cc-developers)
- [Visual Studio Code](https://code.visualstudio.com/)
[block:api-header]
{
  "title": "Operating System of Development Environment"
}
[/block]
If using an OS on any flavor of linux, you'll be able to follow these tutorials with ease, this includes but is not limited to
- Mac OS
- Ubuntu
- Debian
- Fedora

## Windows
If you are developing on Windows, unfortunately we do not provided powershell ports and instructions at this time. In the future we may append powershell commands. In the mean-time you're best bet is to use a VM with Ubuntu, and set up your development environment inside this VM. If you're an advanced Window's developer familiar with porting Linux instructions, you should encounter minimal issues.