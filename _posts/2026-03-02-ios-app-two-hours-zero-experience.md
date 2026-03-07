---
layout: post
title: "I Built an iOS App in 2 Hours With Zero iOS Experience"
date: 2026-03-02
---

I have a 1-year-old son. If you've ever had a toddler, you know what their day looks like: they find something fun and do it 47 times in a row. Climbing on the couch, off the couch, on the couch, off the couch — for twenty minutes straight. And of course I'm recording all of it, because it's adorable and I'll want proof when he's older.

The problem is sharing these videos. Nobody — not grandma, not my friends, not my WhatsApp group — wants to watch a 3-minute video of a baby doing the same thing on repeat. But a 10-second time-lapse of it? That's gold. That's a highlight reel.

So I wanted a simple tool: pick a video, speed it up, save it. No timeline editing, no filters, no subscriptions. Just fast-forward and done.

So I built one. A native iOS app. From scratch. In about two hours.

I have zero experience with iOS development. I've never written Swift. I don't know AVFoundation, UIKit, or SwiftUI. I couldn't tell you the difference between a `PHPickerViewController` and a `UIViewControllerRepresentable` — and honestly, I still can't fully explain what half the code does.

But the app works. On my iPhone. With a Share Extension, so I can speed up videos directly from the Photos share sheet, right next to AirDrop and Messages.

## The setup

I opened Xcode, created a new project (the default template with Core Data that I didn't need), and then switched to Claude Code.

That's it. That was my entire contribution to the development environment.

## What I told Claude

My first prompt was something like: *"I want a native iOS app that speeds up videos. Minimalistic. I want it in the share sheet context menu alongside Print and AirDrop."*

Claude asked me three questions:
- How should users pick the speed? (Slider)
- What to do with the output? (Save to Photos)
- Standalone app, share extension, or both? (Both)

Then it got to work.

## What happened next

Claude stripped out the Core Data template code I didn't need, created a video picker, built a full processing pipeline using `AVMutableComposition` (whatever that is), and wired up a dark, minimal UI with a speed slider and a "Warp" button.

The first version had a bug — only the beginning of the video was actually sped up. I described what I saw, Claude diagnosed the issue (something about per-track scaling vs. composition-level scaling and explicit frame timing), and fixed it.

Then I asked for the Share Extension. Claude wrote the extension code and walked me through adding the target in Xcode — the one step that genuinely requires clicking through Xcode's UI. The rest was all code.

## The bugs were the interesting part

The app worked immediately with videos I'd received on WhatsApp. But videos I'd recorded on my iPhone? Nothing. I'd pick the video and get bounced straight back to the picker screen.

I described the behavior to Claude. Turns out iPhone-recorded videos are HEVC (H.265), and the default photo picker mode tries to transcode them on the fly — and silently fails. The fix was two lines: set `preferredAssetRepresentationMode = .current` and add fallback video type identifiers.

I never would have figured that out on my own. I didn't even know what HEVC was in this context. But Claude knew the exact failure mode and the exact fix. Thanks Claude.

## What I actually did

Let me be honest about my contribution:

- I described what I wanted
- I tested on my phone and reported what happened
- I said "the speed range should be 2x to 20x instead"
- I said "commit it"
- I dragged a logo PNG into Xcode's asset catalog

That's genuinely it. Every line of Swift was written by Claude. Every architectural decision — how to handle video composition, how to manage the export session, how to structure the extension — was Claude's.

## The result

A working iOS app with:
- A video picker that handles all formats including HEVC
- A speed slider (2x-20x) with a clean dark UI
- Progress tracking during export
- Automatic save to Photos
- A Share Extension that appears in the iOS share sheet
- An app icon

Two hours. Zero prior iOS knowledge.

<div style="display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap;">
  <div style="text-align: center;">
    <img src="/assets/images/video_warp_app.gif" alt="Video Warp app in action — picking a video, adjusting speed, and exporting" style="max-width: 280px; border-radius: 12px;" />
    <p><em>The app: pick a video, set the speed, tap Warp</em></p>
  </div>
  <div style="text-align: center;">
    <img src="/assets/images/share_action.gif" alt="Video Warp share extension in the iOS share sheet" style="max-width: 280px; border-radius: 12px;" />
    <p><em>The Share Extension: speed up videos right from the share sheet</em></p>
  </div>
</div>

## The hardest part? Sharing it.

Here's the ironic thing: building the app was the easy part. Getting it onto my family's phones? That's where I hit a wall.

Apple's ecosystem is famously locked down, and it shows. My options for sharing a personal app with my parents are:

- **TestFlight**: Requires a $99/year developer account, uploading to App Store Connect, and then explaining to my mom what TestFlight is and why she needs to install a separate app to install my app.
- **Direct install from Xcode**: Plug each family member's iPhone into my MacBook one by one. Free accounts limit you to 3 devices and the app expires after 7 days. Cool.
- **App Store**: Full review process, screenshots, privacy policy, and — oh right — it targets beta iOS so Apple won't even accept it right now.

I can AirDrop a photo, a video, a PDF, a contact — but not an app. I just built a perfectly functional, harmless little video tool, and the simplest distribution channel is driving to my parents' house with a USB cable.

It feels like the tooling for *building* personal software has leaped forward by a decade, but the tooling for *sharing* it hasn't moved at all. We can vibe code a native app in an afternoon, but we still can't hand it to someone without jumping through hoops designed for commercial software distribution.

I guess I figured out why web apps are so popular these days.

## What this means

I'm not claiming I'm an iOS developer now. I couldn't maintain this codebase without Claude, and I definitely couldn't debug an AVFoundation pipeline on my own.

But that's kind of the point. I had a simple, personal problem — my kid does funny things on repeat and I want to share snappy time-lapses with the family — and the barrier between "I want this" and "I have this on my phone" was about two hours and a conversation.

I love software that does one thing well. No settings pages with 47 tabs. No onboarding flow. No account creation. No "have you considered upgrading to Pro?" You open it, you do the thing, you close it. That's it. That's the app.

The problem is, nobody builds software like that anymore, because nobody can charge $4.99/month for an app with one button. So instead you get CapCut with its 200 features, 180 of which you'll never touch, and a subscription model that costs more than my electricity bill.

But now, if you know exactly what you want — and I mean *exactly* — you can just... describe it and have it. Video Warp has one screen, one slider, and one button. It does one thing. It does it well. It took two hours. It will never ask me to rate it in the App Store.

That's the future I'm excited about. Not AI replacing developers — but AI letting everyone build the tiny, hyper-specific, does-one-thing-perfectly tools that no company would ever bother making. The long tail of software, finally accessible.

Now if you'll excuse me, my son just discovered he can open and close a drawer. I need to go film twenty minutes of it and turn it into a five-second masterpiece.
