---
layout: post
title: "Cropping PDFs to read them on tablets"
tags: [ebooks,tablets,tools]
last_modified_at: 2022-11-19 16:22:21
---

I read a significant number of books on my tablet. Cropping is a very important (fundamental, I'd say) tool in this context, since reading devices, most of the times, are smaller than the physical form of the book being read.

I've done a lot of experiments, and these are my results.

Content:

- [General Information](/Cropping-PDFs-to-read-them-on-tablets#general-information)
- [Linux Programs](/Cropping-PDFs-to-read-them-on-tablets#linux-programs)
- [Online services](/Cropping-PDFs-to-read-them-on-tablets#online-services)
- [Android apps](/Cropping-PDFs-to-read-them-on-tablets#android-apps)
- [iPadOS apps](/Cropping-PDFs-to-read-them-on-tablets#ipados-apps)
- [Conclusion](/Cropping-PDFs-to-read-them-on-tablets#conclusion)

## General Information

It may take a long time to process some PDFs, so readers who want to try those tools, shouldn't not assume that a program crashes just because it gets stuck for a long time.

## Linux Programs

There are a few options to perform cropping, the most common of which are:

| name                                                       | result         | notes                                      |
| ---------------------------------------------------------- | -------------- | ------------------------------------------ |
| [krop](https://github.com/arminstraub/krop)                | *not usable*   | removes the table of content and bookmarks |
| [PDF Arranger](https://github.com/pdfarranger/pdfarranger) | *not usable*   | removes the table of content and bookmarks |
| `pdfcrop`, from `texlive-extra-utils`                      | *not reliable* | couldn't successfully process my test PDF  |

Essentially, none of the common Linux programs are usable.

## Online services

| name              | result      | notes                                      |
| ----------------- | ----------- | ------------------------------------------ |
| pdf.online (Xodo) | **success** |                                            |
| avepdf.com        | *failed*    | worked on some, but failed on a test PDF   |
| i2pdf.com         | unusable    | seems to fails (hangs, with low CPU usage) |
| deftpdf.com       | unusable    | removes TOC                                |
| pdfresizer.com    | *failed*    | didn't work with test                      |
| sejda.com         | *paid*      | paid; couldn't test                        |
| pdfcandy.com      | unusable    | preview is for the cover only              |
| easepdf.com       | unusable    | preview is for the cover only              |
| hipdf.com         | unusable    | size limit                                 |
| bigpdf.11zon.com  | unusable    | broken interface                           |

One service, pdf.online, worked well! Interestingly, it's provided by the same company that writes the Xodo reader.

Note that I've marked i2pdf as unusable, because it could be very slow, but the CPU occupation is so slow that it's either excessively slow, or simply broken.

## Android apps

I've tried many, but I only remember one:

| name                                                                                 | result       | notes                         |
| ------------------------------------------------------------------------------------ | ------------ | ----------------------------- |
| [Xodo PDF Reader](https://play.google.com/store/apps/details?id=com.xodo.pdf.reader) | *very buggy* | good crop, but very buggy app |

Xodo would be in theory the best reader (even independently of the cropping functionality), however, it's so full of bugs, that I couldn't use it.

## iPadOS apps

None of the apps has usable cropping (or, if they do, they have other issues). One implement automatic cropping, which is fairly useless.

## Conclusion

There is pretty much a single option, although it works well: https://pdf.online (Xodo).

If Xodo PDF Reader wouldn't be extremely buggy, it'd be a great choice, but sadly, it's not the case.

It's annoying having to process PDFs on the computer, then copy them (cropping in the app is much more convenient, in particular, because one may want to do little adjustment), but at least, it makes cropping possible.
