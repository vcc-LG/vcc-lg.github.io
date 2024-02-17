---
layout: post
title:  "When will the solar pay itself back?"
date:   2024-02-17 16:30:06 +0000
categories: solar batteries
---

## Introduction

This post describes the process of determining how much our solar panels and batteries have 'paid themselves back'. This is a common line of thought that people have when purchasing a renewable system like panels. Personally I view the decision to buy them as simply having been the logical choice given situation at the time: we had the money to buy a fairly substantial solar system, and the alternative was to continue to rely entirely upon on-grid electricity. Even though our provider, Octopus, sources a low-ish percentage of its electricity from fossil fuels, it's still about 30%, so continuing to use electricity entirely from Octopus doesn't help us in our goal to move away from fossil fuels entirely.

Nevertheless there is some satisfaction to be found in the idea of a purchase such as this eventually saving you more money than the cost of the thing itself, so I am going to try and work out how far away we are from this point (making hopefully the reasonable assumption they are saving us money at all). I'll explain my calculation processes, simplifications etc. along the way, and link to relevant code in case you want to try something similar!

As an aside, we had various teething problems with the solar and batteries which I won't describe here as it would make things too long and complicated. The issues absolutely reduced the extent to which the kit was saving us money, and I mention it only to imply that having now overcome these issues, our rate of savings is higher than it was for probably the first year or so of having this system.

## Our setup and costs

The house has a gas boiler for hot water and central heating. In late August 2022 we had the following installed:

- SolaX X1 G4 Hybrid 5kW Inverter
- 1 x master and 2 x slave SolaX Triple Power batteries (5.8kWh each, 17.4kWh total)
- 18 x Trina TSM-DE09.05 390W solar panels (7.02kW total)

The total cost for the kit and installation was £12,925.

We went on to have a Marlec Solar iBoost (which is used to heat our hot water tank from both solar and electricity) installed in June 2023. The cost for the unit and installation was about £600.

As mentioned above we are with Octopus, and we are on a dual electricity rate, meaning that we get cheaper electricity between 00:30 and 04:30. We also export a certain amount of electricity when it is very sunny and our batteries are full.

Because of this cheap night time rate, I generally force charge the batteries overnight so that we can use cheaper electricity throughout most (or ideally all) of the day without having to import electricity at the much more expensive day rate. I'm not sure if my thinking on the issue is optimal, but in the less sunny months I think it's ideal to have the batteries finish force-charging at 04:30 with a 100% state of charge (SoC), and for that value to gradually decrease during the day down to 10% (the batteries cannot go below this SoC value) by the time it's 00:30 the next day. If the batteries are at a higher SoC by this time then that is fine because then we'll have to import fewer kWh's to get them back to 100%.

We also have an electric vehicle, a fairly old Renault Zoe with a 22kWh battery, and we typically charge it during this cheap night period. We have a Zappi charger which permits solar excess charging - in other words once the batteries are full then any additional solar power is redirected into the car. However, given that we tend to need the car first thing in the morning, I have found that I can only use this feature if I'm very confident that no one is going to need the car until either the following day or the evening.

Our system is (I think) prioritised such that solar power first goes into the batteries, then once they are full it is used to heat our hot water, and once that is heated to the target temperature then it goes into the car.


## Methodology

The calculation I want to end up with is something like this:

```
avg_savings_per_month = (total_amount_spent - amount_saved)/number_of_months_since_installation
```

The easier part of this is working out how much our energy costs have been since the purchase and installation: it's simply the sum of the data in our bills. Our bills are broken down into electricity and gas costs, and given that our panels, batteries, and iBoost have impacts on both of these readings, we can assume that savings are being made in both costs. It is only the costs of our central heating, which remains entirely dependent on gas, which is unaffected by our equipment.

The much more difficult part is working out what we _would_ have spent had we not made the above purchases.

## What we have spent on energy since buying the equipment

We can get this information from our Octopus bills like this:

![alt text](/images/octopus_payment_sample.png)

So we could theoretically just add each of these values into a spreadsheet and sum it up. However, in doing this we are missing an opportunity to collect information at the same time which we know will we need later, i.e. the raw usage and tariff values. So instead perhaps we can leverage the [Octopus API](https://developer.octopus.energy/docs/api/#consumption) to see if it can help speed up this process for us. Specifically let's see if the electricity consumption endpoint gives us what we need:

```json
"results": [
    {
        "consumption": 0.28,
        "interval_start": "2024-02-16T23:30:00Z",
        "interval_end": "2024-02-17T00:00:00Z"
    },
```
Well... not quite. We have a kWh value but no corresponding tariff to help us calculate the cost to us. Octopus have an endpoint for tariff information but of course we need to know what tariff we were on on a given date for this to be useful. And whilst I am all for overengineering a solution, I believe our best option at this point is to manually walk through every bill and collate the data ourselves. This won't be so painful as we only need to go back to August 2022. For the sake of figuring out data for partial months (and losing only a few days worth of energy data) I will assume the panels were installed and working on 1st September 2022.



