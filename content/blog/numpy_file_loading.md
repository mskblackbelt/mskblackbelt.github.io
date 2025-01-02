---
title: "Opening files with NumPy"
date: 2024-02-06T14:30:13-05:00
tags: [TIL, python, numpy]
---

A new tack I'm taking this semester is to remove the use of [Pandas](http://pandas.pydata.org) from my Physical Chemistry Lab course. Pandas is an excellent tool with _many_ evangelists. After some careful examination (and questions from a colleague), I realized that _my_ reasons for using it the course weren't justified. For the most part, I was using Pandas because it made pretty outputs in a Jupyter notebook… hardly a good reason for introducing a new tool to students already overwhelmed with new tools. In an effort to teach the basics (in this case, Python with NumPy, SciPy, and Matplotlib), I decided to replace my Pandas calls with their more fundamental equivalents. None of this is to day Pandas isn't an excellent tool, only that I didn't want to use very limited course time to teach an additional tool (and introduce more sources of confusion). 

One of my frequent calls to Pandas is in importing a series of spectral data files (UV/Vis absorption or fluorescence). These are tab- or comma-separated files with some sort of header. The header is of predictable length depending on the technique, so by skipping a few rows, the imported data are essentially columns of wavelength and intensity values. In Pandas, the `read_csv()` function is used to read in data, even though it can read in data that isn't comma-separated (pet peeve number one with Pandas). Columnar data can be appended to a Pandas array very easily using the same syntax used to make a new `dict` item (`dict[new_key] = new_value`). This ability to easily create new columns is handy, as data transformations are often necessary. This can, of course, be done using simple NumPy arrays, but I haven't figured out how to add a column to a structured array. 

I'll update this post once I have more to say. 