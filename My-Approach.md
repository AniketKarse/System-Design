# 🏗️ System Design Foundations

> Before designing for millions of users, design your thinking
> correctly.

This document covers the **core prerequisite concepts** you must
understand before diving into large-scale system design.

------------------------------------------------------------------------

# 🟢 Online / Offline System Design

Tracking whether a user is online or offline seems simple --- until you
think deeply.

## ❌ The Naive Approach

If user logs in → set online = true\
If user logs out → set online = false

### 🚨 The Real Problem

What if: - The app crashes? - The internet disconnects? - The system
goes down? - The user force closes the app?

You **cannot guarantee** that an API call will always be made to mark
the user as offline.
