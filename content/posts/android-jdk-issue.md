---
title: "Solving Differing Android Versions When Importing Package Targetting Higher Android Version"
date: 2023-07-21T12:47:00+01:00
draft: false
---

## Differing package versions within solution

When adding/updating a package in your solution that contains a higher target version of android than a project that is referencing that package you may get the following error:

_Java SDK 11.0 or above is required when using $(TargetFrameworkVersion) v12.0.  Note: the Android Designer is incompatible with Java SDK 11.0: https://aka.ms/vs2019-and-jdk-11 then point the JDK folder at later version._

To fix this, you must download the relevant version of the Android JDK. In my instance it was JDK 11.	

Also make sure that the relevant version of the API is installed such as API 31 / Android 12.

Then you must update the target version of android in the project csproj to match that of the new package.

You may only have to fix one or all three of these depending on your project/solution state.


