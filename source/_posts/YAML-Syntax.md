---
title: YAML Syntax
date: 2017-04-16 09:27:47
tags: [Configuration, YAML]
categories: [Dev, YAML]
---

# YAML Ain't Markup Language


Below is an example of an invoice expressed via YAML(tm). Structure is shown through indentation (one or more spaces). Sequence items are denoted by a dash, and key value pairs within a map are separated by a colon.
```YAML
--- !clarkevans.com/^invoice
invoice: 34843
date   : 2001-01-23
bill-to: &id001
    given  : Chris
    family : Dumars
    address:
        lines: |
            458 Walkman Dr.
            Suite #292
        city    : Royal Oak
        state   : MI
        postal  : 48046
ship-to: *id001
product:
    - sku         : BL394D
      quantity    : 4
      description : Basketball
      price       : 450.00
    - sku         : BL4438H
      quantity    : 1
      description : Super Hoop
      price       : 2392.00
tax  : 251.42
total: 4443.52
comments: >
    Late afternoon is best.
    Backup contact is Nancy
    Billsmer @ 338-4338.


# load from yaml to HashMap<T, List<Y>>
map:
  T:
    -
      Y
      Y
      Y
```

![gears](https://philsblog.b-cdn.net/images/gears.png "gears")