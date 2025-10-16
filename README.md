# LoyaltyTokenFactory
A Smart Contract Factory for Decentralized Loyalty Programs on the Base Network.

This repository contains the smart contract factory used to deploy new, unique loyalty tokens (points) for various merchants on the Base blockchain. It leverages the Proxy pattern, using the LoyaltyToken implementation contract to create gas-efficient and upgradeable loyalty tokens.

Deployment Details

The LoyaltyTokenFactory is a crucial component of the Loyal Spark platform, allowing authorized parties to register new loyalty schemes on-chain.

Network

Contract Name

Address

Base

LoyaltyTokenFactory

0x61b154cAE13F2312D33397419195753D3849F858

Contract ABI

The following is the essential Application Binary Interface (ABI) for interacting with the LoyaltyTokenFactory contract:

[{"inputs":[{"internalType":"address","name":"_tokenImplementation","type":"address"}],"stateMutability":"nonpayable","type":"constructor"},{"anonymous":false,"inputs":[{"indexed":true,"internalType":"address","name":"tokenAddress","type":"address"},{"indexed":true,"internalType":"address","name":"merchantAddress","type":"address"},{"indexed":false,"internalType":"string","name":"name","type":"string"},{"indexed":false,"internalType":"string","name":"symbol","type":"string"}],"name":"LoyaltyTokenCreated","type":"event"},{"inputs":[{"internalType":"string","name":"_name","type":"string"},{"internalType":"string","name":"_symbol","type":"string"},{"internalType":"address","name":"_merchantAddress","type":"address"}],"name":"createLoyaltyToken","outputs":[{"internalType":"address","name":"tokenProxy","type":"address"}],"stateMutability":"nonpayable","type":"function"},{"inputs":[],"name":"tokenImplementation","outputs":[{"internalType":"address","name":"","type":"address"}],"stateMutability":"view","type":"function"}]


Key Functions

createLoyaltyToken

The primary function for registering a new merchant and deploying their specific loyalty token.

function createLoyaltyToken(
    string memory _name,
    string memory _symbol,
    address _merchantAddress
) public returns (address tokenProxy)


Parameter

Type

Description

_name

string

The full name of the loyalty token (e.g., "Coffee Points").

_symbol

string

The token's ticker symbol (e.g., "CPT").

_merchantAddress

address

The wallet address of the merchant who will control the newly deployed token. This address is granted the minter/admin role for the new token.

Returns

address

The address of the newly deployed ERC-1967 Proxy (which is the user-facing token address).

tokenImplementation

A public view function to retrieve the address of the underlying, immutable logic contract that all proxies point to.

function tokenImplementation() public view returns (address)


Returns

Type

Description

address

address

The address of the LoyaltyToken (ERC-1155) logic contract.

Events

The factory emits an event upon the successful creation of a new loyalty token. This is essential for off-chain services (like the React front-end) to track and index new tokens.

LoyaltyTokenCreated

event LoyaltyTokenCreated(
    address indexed tokenAddress,
    address indexed merchantAddress,
    string name,
    string symbol
);


Argument

Type

Description

tokenAddress

address

The address of the new proxy contract (the token address).

merchantAddress

address

The merchant address that now owns this token.

name

string

The token's full name.

symbol

string

The token's symbol.

Interaction Guide

To create a new loyalty token, you must connect to the Base network and call the createLoyaltyToken function on the factory address (0x61b154cAE13F2312D33397419195753D3849F858) via your Web3 provider (e.g., MetaMask).
