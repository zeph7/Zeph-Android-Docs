# Android Architecture Components

Android architecture components are a collection of libraries that help you design robust, testable, and maintainable apps. 
Start with classes for managing your `UI component lifecycle` and handling `data persistence`.

* Learn the basics of putting together a robust app with the Guide to app architecture.
* Manage your app's lifecycle. New lifecycle-aware components help you manage your activity and fragment lifecycles. 
  Survive configuration changes, avoid memory leaks and easily load data into your UI.
* Use `LiveData` to build data objects that notify views when the underlying database changes.
* `ViewModel` stores UI-related data that isn't destroyed on app rotations.
* `Room` is a SQLite object mapping library. Use it to avoid boilerplate code and easily convert SQLite table data to Java objects. Room provides compile time checks of SQLite statements and can return RxJava, Flowable and LiveData observables.


# Guide to app architecture

This guide encompasses best practices and recommended architecture for building robust, production-quality apps.

Android apps have a complex structure. A typical Android app contains multiple app components, including activities, fragments, 
services, content providers, and broadcast receivers. You declare most of these app components in your app manifest. The Android OS 
then uses this file to decide how to integrate your app into the device's overall user experience.

Keep in mind that mobile devices are also resource-constrained, so at any time, the operating system might kill some app processes 
to make room for new ones.

Given the conditions of this environment, it's possible for your app components to be launched individually and out-of-order, and the 
operating system or user can destroy them at any time. Because these events aren't under your control, `you shouldn't store any app data 
or state in your app components`, and your app components shouldn't depend on each other.

# Common architectural principles

### Separation of concerns

The most important principle to follow is [separation of concerns](https://en.wikipedia.org/wiki/Separation_of_concerns). It's a common mistake 
to write all your code in an Activity or a Fragment. These UI-based classes should only contain logic that handles UI and operating system 
interactions. By keeping these classes as lean as possible, you can avoid many lifecycle-related problems.

### Drive UI from a model

Another important principle is that you should drive your UI from a model, preferably a persistent model. Models are components that are responsible for handling the data for an app. They're independent from the View objects and app components in your app, so they're unaffected by the app's lifecycle and the associated concerns.

Persistence is ideal for the following reasons:

* Your users don't lose data if the Android OS destroys your app to free up resources.
* Your app continues to work in cases when a network connection is flaky or not available.

By basing your app on model classes with the well-defined responsibility of managing the data, your app is more testable and consistent.

# Recommended app architecture

Structure an app using Architecture Components by working through an end-to-end use case.

Imagine we're building a UI that shows a user profile. We use a private backend and a REST API to fetch the data for a given profile.

### Overview

To start, consider the following diagram, which shows how all the modules should interact with one another after designing the app:

![](https://developer.android.com/topic/libraries/architecture/images/final-architecture.png)

Notice that each component depends only on the component one level below it. For example, activities and fragments depend only on a view 
model. The repository is the only class that depends on multiple other classes; in this example, the repository depends on a persistent 
data model and a remote backend data source.

This design creates a consistent and pleasant user experience. Regardless of whether the user comes back to the app several minutes after 
they've last closed it or several days later, they instantly see a user's information that the app persists locally. If this data is stale, 
the app's repository module starts updating the data in the background.

