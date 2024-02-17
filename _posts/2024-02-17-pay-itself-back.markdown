---
layout: post
title:  "When will the solar pay itself back?"
date:   2024-02-17 16:30:06 +0000
categories: solar batteries
---

## Introduction

This post describes the process of determining how much our solar panels and batteries have 'paid themselves back'. This is a common line of thought that people have when purchasing a renewable system like panels. Personally I view the decision to buy them as simply having been the logical choice given situation at the time: we had the money to buy a fairly substantial solar system, and the alternative was to continue to rely entirely upon on-grid electricity. Even though our provider, Octopus, sources a low-ish percentage of its electricity from fossil fuels, it's still about 30%, so continuing to use electricity entirely from Octopus doesn't help us in our goal to move away from fossil fuels entirely.

Nevertheless there is some satisfaction to be found in the idea of a purchase such as this eventually saving you more money than the cost of the thing itself, so I am going to try and work out how far away we are from this point (making hopefully the reasonable assumption they are saving us money at all). I'll explain my calculation processes, simplifications etc. along the way, and link to relevant code in case you want to try something similar!

## Our setup and costs

The house has a gas boiler for hot water and central heating. In August 2022 we had the following installed:

- SolaX X1 G4 Hybrid 5kW Inverter
- 1 x master and 2 x slave SolaX Triple Power (5.8kWh each, 17.4kWh total)
- 18 x Trina TSM-DE09.05 390W solar panels (7.02kW total)

The total cost for the kit and installation was £12,925.

We went on to have a Marlec Solar iBoost (which is used to heat our hot water tank from both solar and electricity) installed in June 2023. The cost for the unit and installation was about £600.

As mentioned above we are with Octopus, and we are on a dual electricity rate, meaning that we get cheaper electricity between 00:30 and 04:30. We also export a certain amount of electricity when it is very sunny and our batteries are full.

Because of this cheap night time rate, I generally force charge the batteries overnight so that we can use cheaper electricity throughout most (or ideally all) of the day without having to import electricity at the much more expensive day rate. I'm not sure if my thinking on the issue is optimal, but in the less sunny months I think it's ideal to have the batteries finish force-charging at 04:30 with a 100% state of charge (SoC), and for that value to gradually decrease during the day down to 10% (the batteries cannot go below this SoC value) by the time it's 00:30 the next day. If the batteries are at a higher SoC by this time then that is fine because then we'll have to import fewer kWh's to get them back to 100%.

We also have an electric vehicle, and so




## Methodology

The calculation I want to end up with is something like this:

```
avg_savings_per_month = (total_amount_spent - amount_saved)/number_of_months_since_installation
```

The easier part of this is working out how much our energy costs have been since the purchase and installation: it's simply the sum of the data in our bills. Our bills are broken down into electricity and gas costs, and given that our panels, batteries, and iBoost have impacts on both of these readings, we can assume that savings are being made in both costs. It is only the costs of our central heating, which remains entirely dependent on gas, which is unaffected by our equipment.

The much more difficult part is working out what we _would_ have spent had we not made the above purchases. Unfortunately we can't just look at the logs of our solar/battery system and look at 'kWh generated' and assume that this can directly translate to energy we would have purchased from Octopus. For example, if on a very sunny day I can see that I exported 7kWh and used


## What we have spent

The total cost for the equipment and installation was



You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

Jekyll requires blog post files to be named according to the following format:

`YEAR-MONTH-DAY-title.MARKUP`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file. After that, include the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
