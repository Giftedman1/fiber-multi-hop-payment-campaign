
# Fiber Multi-Hop Payment Campaign

**Campaign:** Build on CKB — Campaign #7  
**Project:** Send Your First Multi-Hop Payment with Fiber  
**Participant:** [Giftedman1](https://github.com/Giftedman1)

## Overview

This repository documents my completion of the Fiber multi-hop payment tutorial. The exercise demonstrates how Fiber enables payments between two nodes through an intermediary node, even when the sender and receiver do not have a direct payment channel.

The tutorial involved two transactions:

1. Sending 1 CKB from Sender A to Receiver C through Bottle B.
2. Reversing the payment by sending 1 CKB from Receiver C back to Sender A through Bottle B.

## Payment Route

Both transactions used the following multi-hop route:

```text
Sender A → Bottle B → Receiver C
```

For the reverse payment, the direction was:

```text
Receiver C → Bottle B → Sender A
```

## Quest 1: Sender A to Receiver C

I generated an invoice from Receiver C and initiated a payment of 1 CKB from Sender A.

**Transaction outcome:**

| Detail | Result |
|---|---|
| Sender | Sender A |
| Intermediary | Bottle B |
| Receiver | Receiver C |
| Amount received | 1 CKB |
| Payment status | Paid |
| Actual routing fee | 0.005 CKB |
| Maximum allowed fee | 1 CKB |

**Payment hash:**

```text
0xc6e50e1d7d8ad181891aa7c541202b3f869f5037c806d735fcd49a1bba8821c5
```

### Quest 1 Evidence

![Quest 1 payment completed](screenshots/quest-1-payment-completed.png)

## Quest 2: Reverse Payment from Receiver C to Sender A

For the second quest, I reversed the payment direction and sent 1 CKB from Receiver C through Bottle B to Sender A.

The payment was successful, and Sender A received 1 CKB. The actual routing fee was 0.005 CKB, while the maximum allowed fee was 1 CKB.

### Liquidity Before and After

The channel liquidity indicators changed as follows:

| Liquidity indicator | Before | After |
|---|---:|---:|
| Outbound from A | 398.995 CKB | 399.995 CKB |
| Inbound to A | 152.005 CKB | 151.005 CKB |
| Inbound to C | 150 CKB | 151.005 CKB |
| Outbound from C | 401 CKB | 399.995 CKB |
| Maximum invoice for C | 150 CKB | 151.005 CKB |

### Quest 2 Evidence

**Liquidity before the reverse payment**

![Liquidity before reverse payment](screenshots/quest-2-liquidity-before.png)

**Reverse payment confirmation and updated liquidity**

![Reverse payment confirmation](screenshots/quest-2-reverse-payment-confirmation.png)

## Technical Explanation: How the Reverse Payment Changed Liquidity

Before the reverse payment, the liquidity indicators showed 398.995 CKB outbound from A, 152.005 CKB inbound to A, 150 CKB inbound to C, and 401 CKB outbound from C.

After sending 1 CKB back from Receiver C through Bottle B to Sender A, the figures changed to 399.995 CKB outbound from A, 151.005 CKB inbound to A, 151.005 CKB inbound to C, and 399.995 CKB outbound from C.

The reverse payment redistributed liquidity across both channels. Receiver C's inbound liquidity increased from 150 CKB to 151.005 CKB, raising its maximum invoice capacity by 1.005 CKB. This means C can receive another payment of a larger amount.

The actual routing fee was 0.005 CKB, compared with the maximum allowed fee of 1 CKB. The payment demonstrated how multi-hop transactions can move funds through an intermediary while changing the available liquidity in the channels along the route.

## Personal Reflection

Completing this tutorial helped me understand how Fiber enables payments between two nodes that do not have a direct payment channel. I learned that a payment can pass through an intermediary node, such as Bottle, as long as there is sufficient liquidity along the route.

One interesting thing I learned is that opening a channel does not automatically mean that the same amount can be sent and received in both directions. The direction and distribution of liquidity determine whether a payment can succeed.

I found the reverse payment exercise particularly useful because I could observe how sending 1 CKB back from Receiver C to Sender A changed the liquidity in both channels. Receiver C's maximum invoice capacity increased from 150 CKB to 151.005 CKB.

I also learned that the actual routing fee can be much lower than the maximum fee allowance. In both payments, the actual fee was 0.005 CKB, compared with the maximum allowance of 1 CKB.

Working through the tutorial helped me understand the relationship between payment routing, intermediary nodes, channel liquidity, and transaction fees. I can see multi-hop payments being useful for peer-to-peer transfers, merchant payments, and applications where users need to transact without opening direct channels with everyone.

## Conclusion

This exercise provided practical exposure to Fiber's multi-hop payment process, including invoice generation, payment routing, successful transaction confirmation, and channel liquidity changes.

Both payment directions were completed successfully, demonstrating how an intermediary node facilitates transactions between nodes through established payment channels.
