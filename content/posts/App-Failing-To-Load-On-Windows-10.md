+++
title = 'App Failing to Load the second time on Windows 10'
date = 2024-09-30T18:01:46+01:00
draft = true
+++

### Background

We have a Universal Windows Platform (UWP) application that relies heavily on numerous custom-built libraries for various functionalities such as storage access and other operations.

Initially, this UWP application was designed to be compatible with both Windows 8 and Windows 10. However, we have since updated it to support the more recent versions of Windows, specifically Windows 10 and Windows 11.

Despite these updates, some of the custom libraries still contain legacy code that ensures compatibility with Windows 8. This legacy code in many cases may not be necessary anymore and could potentially be optimized or removed.

Our current focus is on enhancing the performance of our UWP application, with a particular emphasis on improving the efficiency of the logging mechanism. We believe that by refining the logging process, we can achieve better overall performance and responsiveness in our application.

### Problem Area

Upon investigation of our logging library we noticed that it was:

- Opening a log file
- Creating a temp log
- Reading the entire contents
- Writing the extra log line
- Closing the file
- Overwrites the existing file with the temporary one

This approach involves repeatedly opening and closing the file, with each operation taking between 1-3 seconds. This was significantly impacting performance.

We decided that to improve our logging performance we would make it so the file stays open for the lifetime of the app. So that's the first change we made, we implented FileRandomAccessStream to create a stream for the logging, tested it all ourselves, found it worked and sent it off to test.

To enhance logging performance, we decided to keep the log file open for the application's lifetime. We implemented `FileRandomAccessStream` to create a persistent stream for logging. After thorough developer centric testing, we confirmed it worked and gave it to our test team.

However, a few weeks later, our test team reported an issue on Windows 10, an OS still used by some of our clients. If the application was closed and then quickly reopened, it would hang and fail to load.

### Finding the Problem

This issue was quite concerning, so we immediately began addressing it. Team members set up Windows 10 virtual machines and installed Windows 10 on several laptops for testing.

We took a step back and asked ourselves: what changes in the code could have caused this regression, and why is it only occurring on Windows 10?

In terms of code, we are now keeping the connection to the log file open longer than before. However, we assumed that this connection would be terminated by the time the app was reopened.

Diagnosing the issue without debugging was challenging, as the broken code was responsible for generating our client logs.

We attached a debugger and set off looking at the output where we noticed an exception. The log file was being accessed whilst it still had a handle open which means it was throwing a conflict exception.

Ok! We've got an error to work with, but it still raised the question... why was this only on Windows 10? It made no sense to us at the time.

Eventually, after extensive testing, we managed to replicate the issue on Windows 11 as well.

### The Fix

We determined from the exception that something was keeping the connection open longer than we needed. So, we decided to investigate which processes were active and discovered the culprit: the RuntimeBroker. This Windows process manages permission access between UWP apps and Windows.

Aha! We found the issue, but how do we ensure the broker stops meddling with our file?

Our first idea was to create an alternative log file if the main one was busy. This would prevent hangs but felt more like a workaround than a proper fix.

Then, while scouring Stack Overflow, we stumbled upon a gem of a comment. It mentioned a .NET class that seemed perfect for our needs: `FileStream`! By using `FileStream`, we could bypass the RuntimeBroker entirely. The file access would be managed by the UWP app process itself, ensuring the handle is closed when the app exits.

Interestingly, the reason this issue wasn't as severe on Windows 11 was because the RuntimeBroker was quicker at closing the connection.

### Conclusion

In the end, we crafted a solution that was far more efficient than our initial approach. This experience underscores the critical importance of testing your application across all supported operating systems. Yet, I can't shake the feeling that we might have missed this issue entirely, given its obscure nature.
