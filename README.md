# Orderbook

A limit order book written in C++ that supports multiple order types and matches buy and sell orders by price-time priority.

Based on / inspired by [Tzadiko/Orderbook](https://github.com/Tzadiko/Orderbook)
Followed original creator's tutorials provided by @TheCodingJesus YouTube channel.

## Features

- Add, cancel, and modify orders
- Order types: [Good Till Cancel, Fill And Kill, Fill Or Kill, Good For Day, Market]
- Price-time priority matching (best price first, then earliest order)
- Aggregated bid/ask level info (price and total quantity per level)
- Trade reporting (which orders matched, at what price and quantity)
- Unit tests

## Order types

Good Till Cancel: Stays in the book until filled or cancelled
Fill And Kill: Fills whatever it can immediately; the remainder is cancelled
Fill Or Kill: Fills completely immediately, or is rejected entirely
Good For Day: Stays in the book until the end of the trading day
Market: Executes immediately at the best available price

## How it works

- Bids and asks are stored in sorted maps keyed by price.
- Each price level holds a FIFO queue of orders, which gives time priority.
- Matching runs after every add and trades while the best bid >= best ask.
