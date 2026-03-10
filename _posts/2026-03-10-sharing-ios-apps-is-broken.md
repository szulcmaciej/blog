---
layout: post
title: "Sharing Private iOS Apps Is Broken"
date: 2026-03-10
tags: [ios, apple, rant, vibe-coding]
excerpt: "I can AirDrop a photo, a video, a PDF, a contact — but not an app. The tooling for building personal software has leaped forward by a decade, but sharing it hasn't moved at all."
---

Last week I was at a playground with my son. He discovered the outdoor workout area and was running in circles around the equipment — and I was filming it, because of course I was. I wanted to turn it into a quick time-lapse and send it to the family group chat. I have an app for that. I [built it myself]({% post_url 2026-03-02-ios-app-two-hours-zero-experience %}) a week ago with Claude Code.

I opened my phone and the app was gone.

Not gone as in deleted. Gone as in *expired*. Because I built it with a free Apple developer account, and free accounts give you apps that self-destruct after 7 days. My perfectly functional, harmless little video tool just... stopped existing. On my own phone.

I rebuilt it that evening — plugged in the phone, opened Xcode, hit build. But of course it wasn't that simple. Xcode first had to rebuild some device support cache or symbol index or whatever it was — several minutes of progress bars before it would even talk to my iPhone. Then the actual install took seconds. So the workflow for using my own app on my own phone is: wait for Xcode to do mysterious housekeeping, build, repeat weekly. Cool.

But it got me thinking about the bigger problem I'd been stewing over since I first built this thing: I wanted to share it with my family, and Apple makes that essentially impossible.

## The options

Apple gives you roughly three ways to share a personal app with your family:

- **TestFlight**: Requires a $99/year Apple Developer Program membership. You upload your app to App Store Connect, wait for processing, then send an invite link. The recipient needs to install TestFlight (a separate app) to install your app. For a video tool I built for my family.
- **Direct install from Xcode**: Plug the target iPhone into your MacBook with a cable, trust the device, and build directly to it. With a free account you're limited to 3 devices, and the app expires after 7 days. So every week you get to plug in every device and rebuild. As I just learned the hard way.
- **App Store**: Full review process, screenshots, metadata, a privacy policy, age ratings, and assuming your app even qualifies. Mine targets a beta iOS version, so Apple wouldn't accept it right now anyway.

That's it. Those are the options.

I can AirDrop a photo, a video, a PDF, a contact, a website link, a Wi-Fi password — but not an app. The one thing I actually *built* is the one thing I can't easily hand to someone.

## This never used to matter

For decades, the difficulty of sharing apps didn't matter much, because the difficulty of *building* them was the real bottleneck. If you could write a native iOS app, you were a professional developer and the $99/year fee was a rounding error. TestFlight's UX was fine because your testers were other developers or QA people who already had it installed.

But the world has changed. AI-assisted coding has collapsed the barrier to building software. People with zero programming experience can now describe what they want and get a working app. The "builder" population has exploded overnight — and Apple's distribution model still assumes that every app is headed for the App Store.

## The gap

Think about what happened in the last few years:

- **Building** a native app went from months → weeks → hours → a conversation
- **Sharing** a native app is still: pay $99, upload to Apple's servers, wait for processing, explain TestFlight to your mom, hope she doesn't accidentally delete TestFlight in six months

The tooling for *creating* personal software has leaped forward by a decade. The tooling for *distributing* it hasn't moved at all.

We're in this weird moment where I can vibe-code a native app in an afternoon but I still can't hand it to someone without jumping through hoops designed for commercial software distribution. The simplest distribution channel for my little family video tool is literally plugging in a USB cable every 7 days.

## What I actually want

I don't want to put my app on the App Store. I don't want strangers downloading it. I don't want to write a privacy policy for a video speed-up tool that maybe my wife and my brother will use.

I just want something like:

> *Generate a link. Send it to 3 people. They tap it, the app installs. Done.*

Or better yet — AirDrop. I can AirDrop literally anything *except* the thing I actually made. Let me AirDrop an app to my wife's phone. She taps "Accept." It installs. That's it.

Apple could gate this behind Family Sharing. They could limit it to 5 devices. They could require the sender to have a verified Apple ID. They could sandbox it harder than App Store apps. Fine. Just give me *something* that doesn't involve explaining what TestFlight is over a phone call.

## Why it matters now

This isn't a niche complaint anymore. As AI makes building apps trivially easy, the number of people hitting this wall is going to explode. Every person who uses Claude, Codex, or any AI coding tool to build a personal iOS app will eventually try to share it — and every single one of them will hit the same wall I did.

The personal software revolution is here. People are building tiny, hyper-specific tools for themselves and their families. But Apple's distribution story still assumes every app is a business.

Android, for all its faults, gets this right. You can just... send someone an APK. They install it. Maybe they tap through a "unknown sources" warning. Done. It's not elegant, but it's *possible*.

On iOS, the locked-down model made sense when apps were built by companies for millions of users. It makes less sense when apps are built by a parent for three family members.

## The irony

The thing that kills me is that Apple positions itself as the platform for creativity. "Built on iPad." "Shot on iPhone." They celebrate what people create — as long as what you create isn't software.

Build a song in GarageBand? Share it anywhere. Paint something in Procreate? Export it however you want. Build an app in Xcode? Welcome to a $99/year bureaucratic maze.

I love the Apple ecosystem. I'm writing this on a Mac, I built the app in Xcode, it runs on my iPhone. But the gap between "I made this" and "my family can use this" shouldn't require an annual subscription and a developer portal.

I guess this is why web apps are so popular. No App Store review. No TestFlight. No $99/year. Just a URL. Maybe the real answer to personal iOS apps is to not build iOS apps at all — just build a PWA and call it a day.

But that feels like giving up. Native apps are better for some things. My video tool uses AVFoundation, the share sheet, the Photos library. A web app can't do that. I *should* be able to build native personal software and share it with my family without filing paperwork.

Apple, if you're listening: the age of personal software is here. Your distribution model needs to catch up.
