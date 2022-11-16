---
layout: post
title: "Choosing components to optimally charge a laptop via USB-C"
tags: [lenovo,hardware,usb-c,yoga]
last_modified_at: 2022-11-16 12:48:21
---

I thought that buying a good USB-C charger and cable would be enough to charge my laptop (a Lenovo Yoga 7 AMD Gen 7), but turns out this is not enough. In this brief article I'll describe the experience and my suggestions.

Content:

- [Context](/Choosing-components-to-optimally-charge-a-laptop-via-USB-C#context)
- [First attempt](/Choosing-components-to-optimally-charge-a-laptop-via-USB-C#first-attempt)
- [Solution](/Choosing-components-to-optimally-charge-a-laptop-via-USB-C#solution)
- [Other devices](/Choosing-components-to-optimally-charge-a-laptop-via-USB-C#other-devices)
- [Conclusion](/Choosing-components-to-optimally-charge-a-laptop-via-USB-C#conclusion)

## Context

When charging a (relatively) high-powered device, there are three components at play:

- the charger,
- the cable,
- the device.

This is less trivial than it seems, since one would assume that a good cable would be enough, but it isn't.

Charging, via USB-C, has different protocols. The standard USB is called "Power Delivery" ("PD"); the most common versions are 2.0 and 3.0, where the latter adds more information about the charging.

My laptop, a [Lenovo Yoga 7 AMD Gen 7](https://www.lenovo.com/lt/lt/laptops/yoga/yoga-2-in-1-series/Yoga-7-Gen-7-14%E2%80%B3-AMD/p/LEN101Y0016), has a 65W PD 3.0 charger; when I plug it, the laptop charges at roughly 50W (measured by the Linux tool [battop](https://github.com/svartalf/rust-battop)).

## First attempt

I purchased an [Anker 715 Charger (Nano II 65W)](https://www.anker.com/products/a2663?variant=41093880250518), and an [Anker Powerline+ III USB C to USB C (60W) cable](https://www.anker.com/uk/products/a8863).

Neither the charger nor the cable descriptions mention anything about the PD standard; the cable description is actually somewhat misleading, because it describes it as "High-Speed Compatible", which makes the user think that it's enough to charge devices that use less than its rated 60W.

This configuration unfortunately lead to a significantly underpowered charging: approximately 30W.

It took me a while to find the specifications, that Anker doesn't report:

- the charger is PD 3.0;
- the cable is PD 2.0.

What's confusing is that there are some reports around that PD 3.0 doesn't make a significant difference, so it was confusing why this was happening.

## Solution

I've then purchased a [Ugreen 100W USB C to USB C cable](https://eu.ugreen.com/products/ugreen-100w-usb-c-to-usb-c-cable).

This solution works - the laptop now charges at the same speed as the original charger (approx. 50W).

Also Ugreen is poor on specifications, but I've found that this cable is PD 3.0.

## Other devices

With the charger above, but cables charge my phone and tablets rapidly, so the only problem has been the laptop.

## Conclusion

If one needs to charge a high-powered device, make sure to buy a PD 3.0 charger _and_ cable.

The configuration the worked in my case is:

- [Anker 715 Charger (Nano II 65W)](https://www.anker.com/products/a2663?variant=41093880250518) and
- [Ugreen 100W USB C to USB C cable](https://eu.ugreen.com/products/ugreen-100w-usb-c-to-usb-c-cable).
