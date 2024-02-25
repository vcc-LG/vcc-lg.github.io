---
layout: post
title:  "When will the solar pay itself back?"
date:   2024-02-17 16:30:06 +0000
categories: solar batteries
---

## Introduction

In late August 2022 we had solar panels and batteries installed in our house. This post describes the process of determining how much so far they have 'paid themselves back'. This is a common line of thought that people have when purchasing a home renewables system like panels.

I'll explain my calculation processes, simplifications etc. along the way, and link to relevant code in case you want to try something similar.

As an aside, we had various teething problems with the solar and batteries which I won't describe here as it would make things too long and complicated. The issues absolutely reduced the extent to which the kit was saving us money, and I mention it only to imply that having now overcome these issues, our rate of savings is higher than it was for probably the first year or so of having this system. There was also a misconfiguration of our system that wasn't rectified until quite recently which means that I don't have access to an accurate measure of the total power that the panels have generated, which will mean some more simplifying assumptions in the calculation.

## Our setup and costs

The house has a gas boiler for hot water and central heating. We have this equipment:

- SolaX X1 G4 Hybrid 5kW Inverter
- 1 x master and 2 x slave SolaX Triple Power batteries (5.8kWh each, 17.4kWh total)
- 18 x Trina TSM-DE09.05 390W solar panels (7.02kW total)

The total cost for the kit and installation was £12,925.

We went on to have a Marlec Solar iBoost (which is used to heat our hot water tank from both solar and electricity) installed in June 2023. The cost for the unit and installation was about £600.

As mentioned above we are with Octopus, and we are on a dual electricity rate, meaning that we get cheaper electricity between 00:30 and 04:30. We also export a certain amount of electricity when it is very sunny and our batteries are full.

The way the systems operate changes depending on the time of year. In the less sunny and colder months I force charge the batteries to 100% overnight during the cheap rate, and I also time the iBoost to heat the water throughout the cheap rate (although the thermostat will kick in once it's reach its target temperature some time during this period). The gas boiler will be used infrequently to top up hot water later in the day as needed, and of course the gas is used for the central heating.

In the sunnier months the iBoost will not come in the night, and instead excess solar energy will be enough to have a full tank of water by the early afternoon (if not sooner). I will reduce the target state of charge for the force charging of the batteries to around 50% so that we have some battery power to last us until the panels are generating plenty of power for the house and we don't dip into the more expensive day rate electricity.

We have an electric vehicle, a fairly old Renault Zoe with a 22kWh battery, and we typically charge it during this cheap night period. We have a Zappi charger which permits solar excess charging - in other words once the batteries are full then any additional solar power is redirected into the car. However, given that we tend to need the car first thing in the morning, I have found that I can only use this feature if I'm very confident that no one is going to need the car until either the following day or the evening.

## Methodology

We need to know the following things:

Since the installation...
- How much have we spent on electricity? (`actual_spend_electricity`)
- How much have we spend on gas? (`actual_spend_gas`)
- How much would we have spent on electricity? (`predicted_electricity`)
- How much would we have spent on gas? (`predicted_gas`)

The value of 'how much has it paid itself back' is then:

```
electricity_saving = actual_spend_electricity - predicted_electricity
gas_saving = actual_spend_gas - predicted_gas
total_saving = electricity_saving + gas_saving
amount_paid_back = cost_of_system - total_saving
```

The easier part of this is working out how much our energy costs have been since the purchase and installation: it's simply the sum of the data in our bills. Our bills are broken down into electricity and gas costs, and given that our panels, batteries, and iBoost have impacts on both of these readings, we can assume that savings are being made in both costs. It is only the costs of our central heating, which remains entirely dependent on gas, which is unaffected by our equipment.

The much more difficult part is working out what we _would_ have spent had we not made the above purchases.


### actual_spend_electricity



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



