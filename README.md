# Avitext: A Standard Shorthand Text Notation Specification for Bird Species Observations

##### Version 1.0.0 Specification

*by Robert Gerald Porter*

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

## Table of Contents
1. [Introduction](#Introduction)
	+ [Assumed Knowledge](#Assumed-Knowledge)
	+ [Process](#Process)
- [Basic Avitext Notation](#Basic-Avitext-Notation)
	+ [Location](#Location)
	+ [Date, Time, Length, Distance](#DateTime)
	+ [Species Observed](#Species)
	+ [Valid Short Codes](#Valid-Short-Count-Codes)
- [Benefits Over Other Methods](#Benefits-Over-Other-Methods)
- [Advanced Avitext Notation](#Advanced-Avitext-Notation)
- [Tips & Tricks](#Tips-Tricks)
- [Limitations](#Limitations)
- [Roadmap](#Roadmap)
- [License](#License)
- [Version](#Version)
	+ [Version History](#Version-History)

<div id='Introduction'/>
## Introduction

**Avitext** is a plain text file format specification for bird species observations in the [ABA region](http://listing.aba.org/descriptions/). It is designed to document checklists in the field as quickly as possible using a smartphone note-taking text application, such as iOS's *Notes* or Google's *Keep* app. 

<div id='Assumed-Knowledge'/>
### Assumed Knowledge

To use this shorthand, you will need to know the standard avian [banding codes](http://help.ebird.org/customer/portal/articles/1987817-using-ebird-four-letter-codes?t=433603). If you do not know them already, they are reletively easy to learn. Most follow a predictable pattern so long as you are aware of the full species name, though a few have special rules. 

If you're unfamiliar with banding codes, using the Avitext specification can be a great way of learning banding codes quickly.

<div id='Process'/>
### Checklist Process
 1. Write checklists, usually while in the field
 - Paste them into a parser
 - Generate a .csv file from the parser
 - Import .csv file to eBird
 - See your checklists on eBird!

<div id='Basic-Avitext-Notation'/>
## Basic Avitext Notation
This example is designed to help you get started right away, and contains all the basic features of the format.

```
ONCA Cootes Paradise
02-15-16 17:05 15 1.2km
BCCH 1 6 2m "males singing"
BLJA 5
DCCO 2 1 6
CARW 1
NOCA 2f 1m 6 "courting behaviour observed"
BEKI 1f 2m "photos taken"
BAEA 1 "flyover" 1i "2nd year immature"
CEDW 160 "min count, largest flock I've seen since 2013"
RBGU 150 "large flock on ice, est"
CAGO 227 25 305 "flyovers headed west, exact"
BLJA 1
PIWA x "newly excavated nesting cavity found"
EABL "not found"
```

<div id='Location'/>
### Line 1: Location Name


```
ONCA Cootes Paradise
```

This is simply a code for your province/state and the the name you wish to give to the location where you are observing. For importing to eBird, this is the hotspot or personal location name. 

`ONCA` in this case refers to the province of Ontario within Canada. Another example would be `NYUS` (New York, USA). Outside of the US or Canada, eBird has a list of "sub-nation" codes that can be used, which tend to be two-letter national code followed by a dash, then the sub-national 3-character code. See [State and Country Codes](http://help.ebird.org/customer/portal/articles/973915-uploading-data-to-ebird) on the eBird website to download a list of them. The parser will understand both styles of codes, for example, either `QCCA` or `CA-QC` for Québec, Canada -- if there's a dash, it should be country first.

For the exact location if you do not type it exactly as the hotspot/personal location is named (including spaces and letter case), you will need to assign the name you give to it to be an alias for the actual hotspot during import process to eBird.

For example, if one were to instead label this as `Cootes Paradise` (which is easier to type), upon import eBird will ask you what hotspot to assign checklists with the location `Cootes Paradise` to, and it will remember in the future that it refers to `Hamilton--Cootes Paradise Sanctuary`.

<div id='DateTime'/>
### Line 2: Date, Time, Length, Distance


```
02-12-16 17:05 15 1.2km
```

This translates as follows: 

 - `02-12-16` as February 12, 2016 format MM-DD-YY. (`02-12` would also be acceptible, the parser will assume the current year -- though this can cause trouble during the new year when importing data from the months previous.)
 - `17:05` as 5:05pm in local time. This must be in 24-hour time.
 - `15` refers to 15 minutes of time observing. (optional; will post to eBird as an "incidental" list if not included)
 - `1.2km` refers to distance covered. Add "k" or "km" for kilometres, without this it will be assumed as miles (optional; will post to eBird as "stationary" if not included. Cannot be added if time observing is not added.)

<div id='Species'/>
### Lines 3+: Observed Species Lines

These lines follow the format of noting first the species in a 4-character banding code, followed by a space, and then as many comments or counts of individuals as necessary (each seperated by a space).

This is best understood by using the example to explain:

`BCCH 1 6 2m "males singing"`
>This refers to a Black-capped Chickadee (`BCCH`), in which 9 individuals were observed. One was observed earlier, probably alone, then six more were seen, and finally two more males (`2m`) were heard singing that were not already observed. 
>
>When this part of the list is run through the parser, it tabulates the full total so you will not need to do math in the field.

---
`BLJA 5`
> This refers to five Blue Jays being observed, with no additional notes referenced.

---
`DCCO 2 1 6 10`
> This refers to Double-crested Cormorants, of which 19 were observed in total. At first, two were seen, then one, then six, then ten. The parser will add these up later.

---
`CARW 1`
> A lone Carolina Wren was observed.

---
`NOCA 2f 1m 4 "courting behaviour observed"`
> This states that 7 Northern Cardinals were observed, 2 of which were female, one of which was male, and 4 others whose sex was not noted or not determined. The additional note states that courting behaviour was observed.

---
`BEKI 1f 2m "photos taken"`
> Three Belted Kingfishers, of which one was female and the other two male. Additionally, the observer noted that they took photos of the birds.

---
`BAEA 1a "flyover" 1i "2nd year immature"`
> This line states that a lone adult Bald Eagle flew over, and then a 2nd year immature Bald Eagle was observed. 

---
`CEDW 160 "min count, largest flock I've seen since 2013"`
> At least 160 Cedar Waxwings, with a note from the observer about the last time such a large flock was seen.

---
`RBGU 150 "large flock on ice, estimate"`

> A hundred and fifty Ring-billed Gulls, noted as being on the ice. Also notes that this is an estimated count.

---
`CAGO 227 25 305 "flyovers headed west, exact"`
>Exactly 557 Canada Geese were observed flying over in three flocks, all headed west.

---
`BLJA 1`
>Another Blue Jay was found, the author forgot it was already on the list. No worries though, this should just be added to the count for this species.

---
`PIWA x "new nesting cavity found"`
>A new Pileated Woodpecker nesting cavity was found, but no Pileated Woodpeckers were directly observed.

---
`EABL "not found at known feeding spot"`
>No Eastern Bluebirds were found. 

>*(***Normally an observer would not include what they didn't see, but this may be relevant if the purpose of the outing was to find this species. eBird does indeed accept zero-counts for this purpose, and the zero count will not cause alerts or appear as a result in species searches.)*

<div id='Valid-Short-Count-Codes'/>
### Valid Short-codes

| Code | Type | Notes
| ------- | :-------- | :---- |
| `m`  | Male | An individual or group of males |
| `f`  | Female | An individual or group of females |
| `j`  | Juvenile | Still in first plumage *(See: ['juvenile' vs 'immature'](http://help.ebird.org/customer/portal/articles/1010509-what-is-the-difference-between-a-juvenile-and-an-immature-))* |
| `i`  | Immature | Not yet a full adult |
| `a`  | Adult | Only necessary if sex is unknown and needs to be differentiated with sub-adults|
| `x`  | Check* | Used to denote occurrance where numbers unknown or not relevant to the observation. This `x` must be without any numerical prefix.


>*Check should only be used when making note of an indirect observations that give evidence of recent presence of a species that has not be observed through direct sight or sound. This might include noting a new nest, identifiable tracks in the snow, or fresh scat. Otherwise, an estimate on the count should be given, to the lowest possible order of magnitude. This is because in eBird "x" could be 1 bird, or 1 million birds -- giving a minimum estimate helps researchers much more.

<div id='Benefits-Over-Other-Methods'/>
## Benefits Over Other Methods

For many, the [eBird mobile app](http://help.ebird.org/customer/portal/articles/1848031-ebird-mobile-apps-overview) is perfectly fine for recording observations -- especially for those who tally their counts after the fact rather than in real time. For those who like to document on-the-fly, however, quickly jotting down notes in this format can be much more efficient than using an app.

Paper & pencil of course have also been time-tested, but would require transcribing in order to import to online or digital systems such as eBird.

One could also just use a note taking app without a standardized format, but that runs the risk of inconsistency and poor readability. 

#### ➤ No doing math in the field!

For real-time recording of bird species, the app currently requires that the user update totals of species manually upon each time it changes. For example, if one was to enter `2` Blue Jays, and then see a third, the user needs to delete the `2`, and replace with a `3`. 

This isn't too hard at the level of single digits, but with species like Canada Geese, having to remove `382`, then do the math manually to figure out that adding `19` more is `401` can be distracting, especially when as you do that calculation, `28` more fly by, then `6` more, then `18`... no more *"...uh, what was the count I just deleted?"*.

Avitext instead is purely additive in nature, a user never needs to delete lines or calculate anything, or memorize what they deleted. Don't worry if you get distracted when a rarity flies past you. The only time you'll be deleting data is to correct mistakes.

#### ➤ No lookup time

Also in most mobile birding apps, the time spent finding a species in the checklist can be time consuming, especially in regions and seasons when diverse species are abundant. With the Avitext method, adding a species is four keystrokes away, no searching needed. Also, you need not memorize taxonomic orders.

#### ➤ Light on resources

Generally speaking, plain text apps are fairly light on a device's memory, storage, and battery life. 

#### ➤ Real-time sharing

Most note taking apps tend to sync up to major cloud platforms instantly when you're online. This means you share an incomplete list for someone to observe in real-time, before it ever reaches eBird.

#### ➤ Works perfectly when remote and/or offline

If you're birding in a remote area with limited or no connectivity, you need not worry as note-taking apps are designed for these kinds of scenarios. 

#### ➤ Compatible with any old device

You can use this format on a tablet without a data connection, an old iPod, or old smartphone that doesn't have a data connection. There's nothing stopping you from using this very format on good old fashioned pen & paper, should your mobile device die on you. This might even work on a smartwatch.

#### ➤ Field-tested since 2012

The author has been using and refining this format since early 2012 for recording observations. Over 2,500 checklists have been converted to almost 300 .csv files for import into eBird over the years using this method.

#### ➤ Review & submit later

For those who don't have time to visit the eBird portal on a daily basis, but are out birding daily, there's nothing stopping you from letting the lists pile up and submitting them all at once a week, a month, or even a year later. Just be sure to review them when submitting!

#### ➤ Transcribe historical lists quicker

The Avitext format works great for transcription work, too. It's even faster to use with a desktop computer & physical keyboard than a mobile device. Some may find this a great improvement than the pointing-and-clicking necessary when transcribing pen & paper checklists directly to the eBird website.

<div id='Advanced-Avitext-Notation'/>
## Advanced Avitext Notation

After you've familiarized yourself with the basic notation, you may want to save yourself a little extra time with the following tricks. 

These are labelled as "advanced" as some of these extra notations have rules and exceptions that you will have to be careful to adhere to.

#### ➤ Make note of "spuhs"

```
[sparrow sp.] 2 "flyovers"
```
Instead of a banding code, you can leave any species description at the beginning of a line between braces (`[ ]`). This species description could be anything, not just "spuhs" (the term used for referring to a group of potential species that a bird could be), and when importing to eBird if it does not match a taxonomy exactly it will ask you what to match it with.

#### ➤ Invalid characters will be parsed as a text comment

Any text outside of quotes that are not the first four characters (the banding code), and are **not preceded by digits**, and are not reserved short-count codes (e.g. `m`, `f`, etc) will be processed as a comment. This makes quotes for comments often unnecessary if you know the caveats below.

**Caveats:** As new aspects of the specification are added to support other short-codes and shorthands, these "invalid characters" may get processed to become something they were not intended to be when initially documented. To avoid this, you should avoid prefixing any words with symbols or punctuation. For example, do not have a comment that is prefixed with `@`, `:`, `(`, `)`, `[`, `]`, `+`, etc, as these might be added to the spec to indicate something specific like a breeding code or as a shorthand to a common comment. These prefixes are however completely safe within double-quotes.

**Always use double-quotes when making a comment that contains numbers. A reference to the year 2015 without this could add 2,015 to your species count!**

#### ➤ Male/female short-codes can be strung together

If you choose you may string together male and female counts with single letters such as `mfmfmmmf`. *This will not work with other markers like `i`, `j`, or `d` as it would be unclear whether these birds were identifiable as male or female as well.*

**Caveats:** Beware of auto-correct on your mobile device trying to correct these to be words. It might just be better to do `m f m f 3m f` to save yourself the risk.

#### ➤ Other short codes can be strung together for an individual or group

This will likely not happen often, but you may choose to denote that two birds are both "male and immature", or "female and adult". These cases **must** be prefixed with a digit for a count though, e.g. `2mi` or `1af`.

### Advanced Example

```
ONCA Cootes Paradise
02-15-16 17:05 15 1.2k
BCCH 1 6 mm males singing
BLJA 5
DCCO 2 1 6
CARW 1
NOCA ff m 6 courting behaviour observed
BEKI fmm photos taken
BAEA 1 flyover 1i "2nd year immature"
CEDW 160 "min count, largest flock I've seen since 2013"
RBGU 150 large flock on ice, est
CAGO 227 25 305 flyovers headed west, exact
UNSP 2
PIWA x newly excavated nesting cavity found
[finch sp.] 2
EABL not found
```

Notes on some of the advanced example lines:

---
`BCCH 1 6 mm males singing`
>Note that quotes are not necessary always. As long as your text does not use words that are only a combination of "m" or "f", and (most importantly) **does not contain numbers**.

---
`NOCA ff m 6 courting behaviour observed`
>Males and females can be referenced with just single or series of `f`s and `m`s, strung together or apart, but must be without quotes. *This does not apply to other codes like "i" (immature), "j" (juvenile), or "a" (adult).*

---
`BEKI fmm photos taken`
>The `m`s and `f`s can be mixed together.

---
`BAEA 1 flyover 1i "2nd year immature"`
>Note that here quotes are necessary due to the number `2` appearing in this comment. Without the quotes, the parser will try to add two more to the total count.

---
`CEDW 160 "min count, largest flock I've seen since 2013"`
>Note again that the quotes here are of utmost importance. Without them, this would be tabulated as 2,193 Cedar Waxwings as `2013` would be added to the count of `160`.

---
`[finch sp.] 2`
>This indicates 2 finches were seen, but the exact species was unknown. 

<div id='Tips-Tricks'/>
## Tips & Tricks

#### ➤ Prepopulate your checklist

If you start a new checklist with several lines with banding codes pre-written for expected species, it'll make things quicker in the field. When using a parser to convert into CSV for upload to eBird, check the option to delete zero-counts if you do not want any missed species referenced as such.

#### ➤ Quick passerine spuh

```
[] 50 unidentified, flyover
```

Use an empty entry with just the braces to indicate unknown passerine species, which the parser will convert to `passerine sp.`. If you wish to indicate "unknown bird" where even the order of the avian species is not known, use `[bird sp.]`.

#### ➤ Hybrid banding codes

```
[ABDUxMALL] 1
```

There are no real banding codes for hybrids, but you could make one up quickly using the brace notation. When you import to eBird, you would just be prompted to assign a valid taxonomy to the code `ABDUxMALL` in this example.


<div id='Limitations'/>
## Limitations

Of course, there are always limitations...

#### eBird import restrictions

eBird's current import methodology (CSV files) has no way to denote sex, age, or breeding codes. When you import any checklist that denotes male or female individuals, for example, the parser will import these counts as comments to be appended to the record, e.g., `5 males, 3 females`.

The only way to deal with this as a user is to go into the checklist after import and manually edit these cases. Also, send the eBird folks a friendly note to improve their import methods :)

There is also no great way to import the CSVs generated by the parser while on a mobile device. You'll need to import to eBird later, when you're on your desktop. The eBird app has the clear advantage here as it can submit directly, right away. Mobile devices are improving every year however, and parsing and submitting to eBird direct from device may be possible quite soon.

#### Quality control

When you import a CSV file to eBird, the system does not request verification of rare species or unusually high counts. This means if you were to make a typo and enter `REDW` (Redwing) instead of `RWBL` (Red-winged Blackbird), you might wake up the whole birding community with alerts that a super-rare Eurasian vagrant has arrived locally when it has not.

This means upon parsing it is important to review lists for any unusual species. You may even opt to click "edit" each checklist after import to eBird to search for the "rare" flag (you have about an hour from submission time before any of your rarities go out on email alerts).

#### Note-taking app features

These days most note-taking apps also come with a lot of fancy things beyond just text -- draw pictures, upload photos, use fonts -- this specification doesn't support any of that, and is unlikely to ever be able to. This specification relies on the simplicity of plain text.

<div id='Roadmap'/>
## Roadmap

Improvements and refinements to the specification are in the works.

These may include: adding standard breeding codes, noting GPS coordinates, nest and egg counts (and NestWatch protocols), specifying custom eBird protocols, recognition of six-letter banding codes, information about bands observed on a bird, support for general checklist comments.

## Technical Specification Notes

>This section is for the technically-minded. Feel free to skip past it.

For the purposes of this table, **lines** are the line number of the text file starting with 1, and **positions** are seperated by spaces starting with position 0, ignoring cases where spaces are part of the text field format.

| Line  | Position  | Format | Description |
|:--:|:--:|---|:---|
|  1 | 0 | `String`  | The state/provincial or sub-national code|
|  1 | 1 | `String`  | The hotspot or personal location name|
| 2 | 0 | `String`  | The date & time in ISO8601 `MM-DD-YY hh:mm` format|
| 2 | 1 | `Number`  | (optional) The number of minutes since the date in position 0|
| 2 | 2 | `Decimal`  | (optional) The number of miles distance covered. Append `km` to indicate kilometres|
| 3... | 0 | `String`  | The banding code taxonomy of species surrounded with braces.|
| 3... | 1... | `String\|Number...` | (optional) A number to add to species count, parseable short-code, or comment | 


<div id='License'/>
## License

This specification is licensed **Creative Commons Attribution 4.0** (CC BY 4.0). See https://creativecommons.org/licenses/by/4.0/ for more info.

<div id='Version'/>
## Version

The current version is **1.0.0**.

This specification uses [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html) ("semver") when tracking spec version changes. 

In short, this means any checklist created with the specification version 1.0.0 will be accepted by parsers and be compatible with checklists based on any 1.x.x version, but may not be compatible with a 2.x.x parser (should there ever be one).

<div id='Version-History'/>
### Version History
 * October 2016: v1.0.0 is published as a draft.
 * December 2016: v1.0.0 has "draft" status removed, [parsing app](https://github.com/rgeraldporter/avitext-to-ebird) is made available.

