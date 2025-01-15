# Objective-C KVO Crash: Observer Not Removed Before Dealloc

This repository demonstrates a common yet easily overlooked bug in Objective-C when using Key-Value Observing (KVO).  Failing to remove observers before the observed object is deallocated can lead to crashes.

The `bug.m` file contains the problematic code. The `bugSolution.m` file provides the corrected implementation.

## Problem

The issue stems from not removing the observer added using `addObserver:forKeyPath:options:context:`.  When the observed object is deallocated, attempting to send messages to a deallocated observer results in a crash.

## Solution

The solution involves removing the observer using `removeObserver:forKeyPath:` within the `dealloc` method of the observer. It's crucial to remove the observer before the observed object is deallocated.  Additionally, error checking ensures that `removeObserver` is only called if an observer has actually been added.