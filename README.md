# Auto Layout by Tutorials: Materials

This repo contains all the downloadable materials and projects associated with the **[Auto Layout by Tutorials](https://store.raywenderlich.com/products/auto-layout-by-tutorials)** from [raywenderlich.com](https://www.raywenderlich.com).

Each edition has its own branch, named `editions/[EDITION]`. The default branch for this repo is for the most recent edition.

## Release History

| Branch                                                                           | Edition | Release Date |
| -------------------------------------------------------------------------------- |:-------:|:------------:|
| [editions/1.0](https://github.com/raywenderlich/alt-materials/tree/editions/1.0) | 1.0     | 2020-05-15   |

## Here are five pros of using storyboard:
* As the name implies, storyboards become a flow diagram. A storyboard makes visualization of the app’s flow vivid and obvious. You can tell by looking at a storyboard that the first view controller transitions to the second view controller with the segue indicator arrow. You can see the UI elements inside of a view controller. Also, available to you with a storyboard is the real-time update of how UI objects appear after constraint updates. These are three examples of the many visual benefits from storyboards.

* Almost every iOS developer learns to construct layouts in storyboards at some point today. Under the circumstance where the storyboard complexity is low, on-boarding a developer into your project is easier in the sense that more developers are well-versed with storyboards than other methods of layout construction. Plus, most developers start out learning to construct Auto Layout constraints using storyboards.

* Apple pushes developers to construct layouts in storyboards with Interface Builder. Historically, Apple has continued to add features, improve upon existing features and provide developer support materials on constructing layouts in Interface Builder. You can expect to continue support from Apple with the development of Interface Builder. Apple has emitted its aura of pushing everyone to learn to code. Using Interface Builder is often dramatically less intimidating than building layouts in other methods like code.

* Building out your layout in the Interface Builder gives you the benefits of Apple’s behind the scene optimization of your layouts.

* Layout changes to your UI objects are reflected in the storyboard. This omits the need to build and run your app to see how your UI objects have changed. Consequently, this saves time.


## Here are five cons of using storyboard:

* The infamous merge conflicts resolution problem. Merge conflicts are easy to come by when two or more developers make changes onto a single storyboard. Because storyboard files are stored as XML, the files are not exactly the most reader-friendly. When there are multiple changes from different developers using the same storyboard file, you may find yourself spending some time resolving merge conflicts. This effect can compound over time. Apple has taken measures to make merge conflicts less of a problem with more readable XML files and by making it easier to split up large storyboard files. However, the storyboard merge conflict problem persists.

* Do you want everything that has to do with the app UI in one place? Interface Builder can be problematic as your app complexity grows. You can set your UI to different values to do different things in Interface Builder with storyboards. However, at the same time, you can also make changes to your UI objects in code. You may wonder why your UI looks completely different on your device than the storyboard. In addition, you may find your app requiring both storyboard and code maintenance instead of one or the other. This can lead to presentation logic ambiguities.

* Re-usability is vital for maintainability. In the scenarios of where you want to build on top of the existing view controller or reuse certain UI elements from a view controller you storyboard, then you are out of luck. The storyboard does not support this.

* Interface Builder is a graphical user interface built as an additional layer for generating XML codes. The additional layer makes Interface Builder prone to UI bugs on the editor and at runtime. The reliability of this layer is dependent on the Xcode team.

* Using Interface builder increases compile time compared to code implementation. As complexity increases in your storyboard files, compile-time can take up a chunk of development time. Consider the compounding effect of development time.


