---
layout: post
title:  "When will the solar pay itself back?"
date:   2024-02-17 16:30:06 +0000
categories: solar batteries
---

## Introduction

This post describes the process of determining how much our solar panels and batteries have 'paid themselves back'. This is a common line of thought that people have when purchasing a renewable system like panels. Personally I view the decision to buy them as simply having been the logical choice given situation at the time: we had the money to buy a fairly substantial solar system, and the alternative was to continue to rely entirely upon on-grid electricity. Even though our provider, Octopus, sources a low-ish percentage of its electricity from fossil fuels, it's still about 30%, so continuing to use electricity entirely from Octopus doesn't help us in our goal to move away from fossil fuels entirely.

Nevertheless there is some satisfaction to be found in the idea of a purchase such as this eventually saving you more money than the cost of the thing itself, so I am going to try and work out how far away we are from this point (making hopefully the reasonable assumption they are saving us money at all). I'll explain my calculation processes, simplifications etc. along the way, and link to relevant code in case you want to try something similar!

## Our setup

- SolaX X1 G4 Hybrid 5kW Inverter
- 1 x master and 2 x slave SolaX Triple Power (5.8kWh each, 17.4kWh total)
- 18 x Trina TSM-DE09.05 390W solar panels (7.02kW total)

This was installed in August 2022. We went on to have a Marlec Solar iBoost (which is used to heat our hot water tank from both solar and )

## Cost

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
