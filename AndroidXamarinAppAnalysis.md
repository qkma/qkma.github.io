title: "Analyzing an Android developed with Xamarin Framework."
date: 2025-03-14
tags: [apk analysis, Xamarin, deobfuscation, traffic interception] # Optional: Add relevant tags
categories: [Reverse engineering, mobile app analysis] # Optional: Add relevant categories

# Introduction

Recently worked on analyzing an Android app that's written with Xamarin framework. This post is to document what I learned from this process. If you are not familiar with Xamarin, from [Wikipedia](https://en.wikipedia.org/wiki/Xamarin), "Xamarin is a Microsoft-owned subsidiary that develops tools and libraries for building apps with C# across multiple platforms." And according to [Microsoft](https://dotnet.microsoft.com/en-us/apps/xamarin), Xamarin support ends May 1 2024. Developers are recommended to migrate to .NET Multi-platform App UI (.NET MAUI).

## Initial analysis
I had apk file of the mobile app. Apk file is nothing more than a zip. A quick unzip will extract file contents out.
```javascript
unzip xamapp.apk
```
After unzipping, besides the usual AndroidManifest.xml, classes.dex, assets, lib, etc, that you will find in an android app, there is a folder called "assemblies" that caught my attention. Inside the folder are a number of dll files.
From google search and Xamarin documentation, these dll files contain the main logic of the mobile app. 

## DLL Handling/Deobfuscation to Get Code
### Decompress
The first thing to do with these dll files is to decompress them with the script provided at https://github.com/NickstaDB/xamarin-decompress. I used the following batch processing script in Windows to decompress all the dll files in place.
```bash
@echo off
set "folder=.\assemblies"
set "program=python decompress.py"

for %%f in ("%folder%\*.dll") do (
  echo Processing %%f
  %program% -o "%%f"
)

echo Done.
```
### 



