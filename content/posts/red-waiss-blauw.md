---
title: "Hail to the Red, Wäiss, and Blauw"
date: 2021-10-27
category: art
tags:
 - art
 - luxembourg
---

## First, A Few Fun Flag Facts

Luxembourg and the Netherlands have nearly identical flags, save for two differences: a slightly different proportion[^1] and a different blue for the bottom stripe. I recently started wondering, though, _how_ different are they?

[^1]: Interestingly, the Luxembourgish flag has two officially accepted proportions -- 1:2 and 3:5 are both considered fine. I don't know of any other countries that do this, though I'm sure someone better versed in vexillology could come up with an example.

The definition of Luxembourg's blue is fairly straightforward. Because no one had really bothered to make the flag official for about a century, the [precise definition](https://legilux.public.lu/eli/etat/leg/rgd/1993/07/27/n2/jo) of the flag wasn't written until 1993 and used Pantone to define its colors, which are then pretty easy to look up sRGB values for.

The Dutch flag is a little trickier. It was formally defined back in 1949, predating Pantone. Here's a translation of [its defintion](https://puc.overheid.nl/doc/PUC_41859_10/1/#8c824c38-7a1e-4b09-a6db-2f10b19ad950):

> When illuminated by standard illuminant C with an incident angle 45 degrees to the surface, the values ​​of the trichromatic coordinates and the trichromatic coefficients when observed in a direction perpendicular to the surface are as follows:
>
>
> |      | X | Y | Z | x[^2] | y[^2] |
> |------|:-:|:-:|:-:|:-:|:-:|
> | __Red__ |18.3|10.0|3.0|0.5847|0.3195|
> | __Blue__ |7.5|6.6|25.3|0.1904|0.1675|
>
> The coordinate system is chosen in such a way that the following applies for an idealized white surface: Y=100.

[^2]: These coefficients just refer to an equivalent reformulation of the CIE XYZ color space called [CIE xyY](https://en.wikipedia.org/wiki/CIE_1931_color_space#CIE_xy_chromaticity_diagram_and_the_CIE_xyY_color_space).

The keen-eyed color nerd will recognize this as probably being the [CIE 1931](https://en.wikipedia.org/wiki/CIE_1931_color_space) color space. [Conversion to sRGB is finicky](https://mina86.com/2019/srgb-xyz-conversion/), but after working through that you can find a good approximation with the color {{< inlineColor 21468B >}}. But what really surprised me is that running this same process on the Dutch red also produces a different red than the Luxembourgish flag, despite usually being referred to as being identical: {{< inlineColor AE1C28 >}} for the Netherlands but the distinctly brighter {{< inlineColor EF3340 >}} for Luxembourg.

The next question for me is how these line up with my native red/white/blue flag, the United States' Old Glory. These used to be defined by a standard textile swatch that bore some resemblance to an old-school Pantone, and seem to have been incorporated into Pantone's palettes. The exact Pantone colors can be found in the State Department's extremely thorough [style guide](https://eca.state.gov/files/bureau/state_department_u.s._flag_style_guide.pdf). After all that, we end up with these lovely hues:

{{< colorSwatch 041e42 "United States" >}} {{< colorSwatch 21468B "Netherlands" >}} {{< colorSwatch 00A3E0 "Luxembourg" >}}

{{< colorSwatch bf0d3e "United States" >}} {{< colorSwatch AE1C28 "Netherlands" >}} {{< colorSwatch EF3340 "Luxembourg" >}}

## Colorimetric Distance

Okay, they're definitely all different colors, but you could probably swap out the American and Dutch red and no one would notice. Is there a good way of measuring the distance between two colors? Enter the lovely [L\*a\*b\* color space](https://en.wikipedia.org/wiki/CIELAB_color_space).

Created by CIE in 1976 (same folks from the XYZ color space used in the Dutch flag), L\*a\*b\* is special because it is uniform, meaning that the euclidean distance between two colors often corresponds pretty closely to how similar two colors appear, called ΔE[^4]. This has a few caveats for strongly saturated colors, but compared to the current [state of the art](https://zschuessler.github.io/DeltaE/learn/#toc-delta-e-2000) its simplicity is worth a fair bit. A value of less than one means they're likely imperceptibly similar, and a value between 2 and 10 usually means they're pretty clearly different at a glance.

[^4]: The E stands for _Empfindung_, German for sensation or impression. You know, just in case 3 Germanic languages weren't enough for one blog post.

Great, so let's convert from sRGB to L\*a\*b\* and find ΔE! This is roughly as finicky as the translation to CIE XYZ with [one more step](https://www.cs.rit.edu/~ncs/color/t_convert.html#XYZ%20to%20CIE%20L*a*b*%20(CIELAB)%20&%20CIELAB%20to%20XYZ) to take us from XYZ to L\*a\*b\*. With that out of the way, we end up with this lovely table:

<!--
L*a*b* coordinates for the blues:
us = (11.6051245051478, 6.36366408685074, -25.5881058989152)
nl = (30.801859490739, 12.5104835757131, -42.2563491156761)
lu = (62.9910637575482, -13.6273706658799, -40.5987237053908)
-->

| Blue   | {{< inlineColor 041e42 US >}} | {{< inlineColor 21468B NL >}} | {{< inlineColor 00A3E0 LU >}} |
|:--:|:--:|:--:|:--:|
| {{< inlineColor 041e42 US >}} | 0 |  26.15  | 57.14 |
| {{< inlineColor 21468B NL >}} |  26.15  | 0 |  41.50  |
| {{< inlineColor 00A3E0 LU >}} |  57.14 |  41.50  | 0 |

You obviously don't need these numbers to tell you that these colors are different from one another, but it's still an interesting exercise. The big thing that sticks for me while doing this calculation is that the Dutch and Luxembourgish blues differ almost purely in luminosity. If you set Luxembourg's L\* value to match the Netherlands, you end up with the near perceptual twin {{< inlineColor "005288" >}}:

{{< colorSwatch 21468B Netherlands >}} {{< colorSwatch "005288" "Dark Lux" >}}

However, the ΔE between these two is a fairly high 26.19 -- supposedly as different as the American and Dutch blues are. I guess this highlights the shortcomings of the dE76 euclidean calculation for color similarity. But if we buckle down and try out the Delta E 2000 (dE00) algorithm, we get ΔE = 17.25, which still feels pretty high to me. I dunno, maybe I just have a bad intuition for these things.

<!--
L*a*b* coordinates for the reds:
us = (40.7547026789377, 64.6645285026816, 23.3372942200762)
nl = (37.810787874328, 56.5290722208815, 32.5610732118348)
lu = (53.0462610075381, 69.7724525339166, 39.1830097769593)
-->

| Red | {{< inlineColor bf0d3e US >}} | {{< inlineColor AE1C28 NL >}} | {{< inlineColor EF3340 LU >}} |
|:--:|:--:|:--:|:--:|
| {{< inlineColor bf0d3e US >}} | 0 |  12.65  | 20.69 |
| {{< inlineColor AE1C28 NL >}} |  12.65  | 0 |  21.24 |
| {{< inlineColor EF3340 LU >}} |  20.69 |  21.24  | 0 |

Again I'm surprised by how high the ΔE is, this time between the US and Netherlands. I could've sworn it would be around 5. (I later ran this using the dE00 algorithm and got a ΔE of 4.72, which feels a lot closer to what I'd expect.)

Anyways, we're done! Well, except...

## Oops, Wrong White Point

All of these conversions between color spaces depend on what exactly we mean when we call something "white." For nearly all modern applications, this refers to a white point known as D65, which is meant to represent the average spectral density of daylight. If you're working with printing processes, you might be working with the slightly different illuminant D50, but _almost_ everyone uses D65 for _almost_ everything. Just about any color converter you'll find online uses D65 implicitly. However, D65 wasn't defined until 1976, long after the Dutch flag was standardized! The Dutch Minister of the Navy really did mean Standard Illuminant C, which was defined by CIE back in 1931 by using an incadescent lightbulb and a special liquid filter to mimic daylight. It turned out that it wasn't a very good model so it's been deprecated ever since the D series was formalized. So, what happens to our color when we account for this? Drumroll please...

{{< colorSwatch 1e4785 "Illuminant C" >}} {{< colorSwatch 21468b "Illuminant D65" >}}

{{< colorSwatch ad1d25 "Illuminant C" >}} {{< colorSwatch AE1C28 "Illuminant D65" >}}

Hm. Not a whole lot, apparently. Algorithm dE00 spits out a ΔE of 0.86 and 1.73, respectively. Still! It's worth being careful with these things. Every Wikipedia article I've seen uses the incorrect D65 illuminant for its sRGB conversion and as far as I can tell, there is zero mention of this corrected color in relation to the Dutch flag anywhere on the internet. I highly doubt that I'm the first person to run these calculations but I can't find anyone else who has documented[^5] it.

[^5]: Just for replication's sake, I ran this calculation with the [colormath python module, version 3.0.0](https://github.com/gtaylor/python-colormath/releases/tag/3.0.0).

It's surprisingly difficult to find an image of the Dutch flag on any central goverment site. The central government has a logo that uses a blue similar to its flag, but as far as I can tell it isn't intended to be identical. Still, even this specification is confusing. It was [at one point specified](https://www.rijkshuisstijl.nl/communicatiemiddelen/bewegwijzering/logo-bewegwijzering) to use {{< inlineColor 123552 >}}, but I think this may be out of date because just about every official website I checked uses {{< inlineColor 154273 >}} instead -- including its own.

Here's what I _could_ find, at least:

- [rvo.nl](https://www.rvo.nl/onderwerpen/internationaal-ondernemen/landenoverzicht/luxemburg/factsheet-luxemburg) has a national factbook that uses slightly-off colors for Luxembourg's flag, and (understandably) lacks a listing for the Netherlands. I did find [this page](https://www.rvo.nl/caribisch) though, which uses the wrong D65-calculated color.
- [ind.nl](https://ind.nl/en/Pages/default.aspx) has a flag in the corner for its language selection, which uses the incorrect colors {{< inlineColor d52b1e >}} and {{< inlineColor 01679a >}}.
- Of the few hundred flags I sampled on Google Images, I didn't find a single one that used the right color. {{< inlineColor 204488 >}} made several appearances, though I'm not exactly sure why.

## Conclusion

This isn't where I expected this question to go! Any question regarding color leads to a functionally infinite rabbit hole to dive down, but this one had a fun historic flair to it that I haven't needed to think about before. How colors are represented in law is also generally a pretty neat topic, and if it's something that piques your interest I recommend digging into the [wild world of trademarked colors](https://www.gerbenlaw.com/trademarks/apparel/tiffany/#75544375). If you're feeling a bit bold you might even decide to to [grab some of these colors](https://culturehustle.com/products/tiff-blue) for yourself and go commit some color crimes :)