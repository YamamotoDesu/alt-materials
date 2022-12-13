# Auto Layout by Tutorials: Materials

This repo contains all the downloadable materials and projects associated with the **[Auto Layout by Tutorials](https://store.raywenderlich.com/products/auto-layout-by-tutorials)** from [raywenderlich.com](https://www.raywenderlich.com).

Each edition has its own branch, named `editions/[EDITION]`. The default branch for this repo is for the most recent edition.

## Release History

| Branch                                                                           | Edition | Release Date |
| -------------------------------------------------------------------------------- |:-------:|:------------:|
| [editions/1.0](https://github.com/raywenderlich/alt-materials/tree/editions/1.0) | 1.0     | 2020-05-15   |

# Here are five pros of using storyboard:
* As the name implies, storyboards become a flow diagram. A storyboard makes visualization of the app’s flow vivid and obvious. You can tell by looking at a storyboard that the first view controller transitions to the second view controller with the segue indicator arrow. You can see the UI elements inside of a view controller. Also, available to you with a storyboard is the real-time update of how UI objects appear after constraint updates. These are three examples of the many visual benefits from storyboards.

* Almost every iOS developer learns to construct layouts in storyboards at some point today. Under the circumstance where the storyboard complexity is low, on-boarding a developer into your project is easier in the sense that more developers are well-versed with storyboards than other methods of layout construction. Plus, most developers start out learning to construct Auto Layout constraints using storyboards.

* Apple pushes developers to construct layouts in storyboards with Interface Builder. Historically, Apple has continued to add features, improve upon existing features and provide developer support materials on constructing layouts in Interface Builder. You can expect to continue support from Apple with the development of Interface Builder. Apple has emitted its aura of pushing everyone to learn to code. Using Interface Builder is often dramatically less intimidating than building layouts in other methods like code.

* Building out your layout in the Interface Builder gives you the benefits of Apple’s behind the scene optimization of your layouts.

* Layout changes to your UI objects are reflected in the storyboard. This omits the need to build and run your app to see how your UI objects have changed. Consequently, this saves time.


# Here are five cons of using storyboard:

* The infamous merge conflicts resolution problem. Merge conflicts are easy to come by when two or more developers make changes onto a single storyboard. Because storyboard files are stored as XML, the files are not exactly the most reader-friendly. When there are multiple changes from different developers using the same storyboard file, you may find yourself spending some time resolving merge conflicts. This effect can compound over time. Apple has taken measures to make merge conflicts less of a problem with more readable XML files and by making it easier to split up large storyboard files. However, the storyboard merge conflict problem persists.

* Do you want everything that has to do with the app UI in one place? Interface Builder can be problematic as your app complexity grows. You can set your UI to different values to do different things in Interface Builder with storyboards. However, at the same time, you can also make changes to your UI objects in code. You may wonder why your UI looks completely different on your device than the storyboard. In addition, you may find your app requiring both storyboard and code maintenance instead of one or the other. This can lead to presentation logic ambiguities.

* Re-usability is vital for maintainability. In the scenarios of where you want to build on top of the existing view controller or reuse certain UI elements from a view controller you storyboard, then you are out of luck. The storyboard does not support this.

* Interface Builder is a graphical user interface built as an additional layer for generating XML codes. The additional layer makes Interface Builder prone to UI bugs on the editor and at runtime. The reliability of this layer is dependent on the Xcode team.

* Using Interface builder increases compile time compared to code implementation. As complexity increases in your storyboard files, compile-time can take up a chunk of development time. Consider the compounding effect of development time.


# Using Xibs

Under the User Interface section, select View and click Next.
![image](https://user-images.githubusercontent.com/47273077/204123154-fb315146-8f80-4cf5-a930-52c041b98930.png)


Select the View and go to the Attributes inspector. On the simulated metrics section, select Freeform for the size attribute.

![image](https://user-images.githubusercontent.com/47273077/204123169-71547e40-993b-4ef9-bd2d-f2ee66c5f121.png)

Now, go to the Size inspector, and set the width and height equal to 150.
![image](https://user-images.githubusercontent.com/47273077/204123176-41081107-f604-48fe-8654-275fcefc26dd.png)

In the same group, add another new file. Select Cocoa Touch Class with UIView subclass and name it ContactPreviewView.

Open ContactPreviewView.xib. Select File’s Owner in the document outline, and go to the Identity inspector. Select ContactPreviewView for the class attribute.

Add the following code, starting at the beginning, inside the ContactPreviewView class in the ContactPreviewView.swift file:

 ```swift
 // 1
override init(frame: CGRect) {
  super.init(frame: frame)
  loadView()
}
// 2
required init?(coder aDecoder: NSCoder) {
  super.init(coder: aDecoder)
  loadView()
}

func loadView() {
  // 3
  let bundle = Bundle(for: ContactPreviewView.self)
  // 4
  let nib =
    UINib(nibName: "ContactPreviewView", bundle: bundle)
  // 5
  let view = nib.instantiate(withOwner: self).first as! UIView
  // 6
  view.frame = bounds
  // 7
  addSubview(view)
}
```
Here’s what you did:

1. Override the init(frame:) constructor so that you can call loadView().

2. Override the required init(coder:) constructor so that you can call loadView(). Since it’s a required constructor, not implementing it will cause an error.

3. Get a reference to the bundle that contains the ContactPreviewView .xib file.

4. Create an instance of the ContactPreviewView .xib, indicating its containing bundle.

5. Instantiate the view and assign the owner, which is the current class.

6. Set view.frame equal to bounds. This gives view the same dimensions as its parent.

7. Add the instantiated view to the current view.

Open ContactListTableViewController.swift (in the Controllers group) and add this code immediately after the cellIdentififer declaration:
```swift
@IBOutlet var contactPreviewView: ContactPreviewView!
```

Open Contacts.storyboard. Press Command-Shift-L and look for uiview.
![image](https://user-images.githubusercontent.com/47273077/204123272-e976c7f4-a04d-40ee-99a6-ea632fd3ea64.png)

Drag the view object below the Exit item in the document outline.
![image](https://user-images.githubusercontent.com/47273077/204123281-da35ee74-fbbb-44fd-8a40-259ecb32827b.png)

Select the view. In the Identity inspector, select ContactPreviewView for the class attribute.

Control-drag from ContactListTableViewController to the ContactPreviewView. An outlets popup will appear; select contactPreviewView.
![image](https://user-images.githubusercontent.com/47273077/204123291-42edf3c5-402d-4a44-94e6-7169b8a2b80c.png)

Go to ContactListTableViewController.swift and type the following code at the end of the class:
```swift
// MARK: - Setup Contact Preview
override func tableView(_ tableView: UITableView, 
    accessoryButtonTappedForRowWith indexPath: IndexPath) {
  // 1
  let contact = contacts[indexPath.row]
  // 2
  view.addSubview(contactPreviewView)
  // 3
  contactPreviewView
    .translatesAutoresizingMaskIntoConstraints = false
  // 4
  NSLayoutConstraint.activate([
    contactPreviewView.widthAnchor.constraint(
      equalToConstant: 150),
    contactPreviewView.heightAnchor.constraint(
      equalToConstant: 150),
    contactPreviewView.centerXAnchor.constraint(
      equalTo: view.centerXAnchor),
    contactPreviewView.centerYAnchor.constraint(
      equalTo: view.centerYAnchor)
  ])
  // 5
  contactPreviewView.transform =
    CGAffineTransform(scaleX: 1.25, y: 1.25)
  contactPreviewView.alpha = 0
  // 6
  UIView.animate(withDuration: 0.3) { [weak self] in
    guard let self = self else { return }
    self.contactPreviewView.alpha = 1
    self.contactPreviewView.transform =
      CGAffineTransform.identity
  }
}

```
<img width="565" alt="スクリーンショット 2022-11-27 16 04 43" src="https://user-images.githubusercontent.com/47273077/204123497-0768ca28-d160-492d-bdc5-c66824b31e3a.gif">


## Pros
* Since .xibs have less UI described in one file, it can be easier to manage or avoid conflicts, compared to storyboards.

* It’s easy to reuse a .xib file throughout a project, to avoid creating duplicated interfaces, or even use them in other projects.

* It can help to have part of the system more encapsulated.

* It shines when you need to create custom controls. If you’re going to use Interface Builder to create custom controls, .xib files are the way to go.

## Cons
* You can’t have relationships between screens, something that’s simple and useful while using storyboards.

* No visualization of the workflow of your app. That’s something you can only have with storyboards.

* If the view is dynamic, it can be difficult to create using .xibs.

# When not to use stack views
Imagine you have a stack view with a left view and a right view. The stack view has a fixed height, and its subviews have equal width. When you animate the right view’s isHidden property from false to true, the stack view animates your views a certain way. The left view will take up the space of the right view as the left view expands, and the right view shrinks. If the animation behavior is not what you want, then you may find manual constraints to be a more suitable solution for the UI you want to achieve.

In addition to the stack view’s behavior expectations, you may be working on a legacy codebase. The legacy codebase may have a pre-iOS 9.0 deployment target. This means that if you use stack views, you would need to support both pre-iOS 9.0 and iOS 9.0 and newer. This is a maintenance consideration that may affect crucial business decisions. This is another example of when stack views can be a less viable solution in comparison to creating additional constraints.

# Launching a view controller from the storyboard in code
Open AppDelegate.swift and replace the code inside application(_:didFinishLaunchingWithOptions:) with the following:
```swift
// 1
let storyboard = UIStoryboard(name: "TabBar", bundle: nil)
// 2
let viewController =
  storyboard.instantiateInitialViewController()
// 3
window = UIWindow(frame: UIScreen.main.bounds)
// 4
window?.rootViewController = viewController
// 5
window?.makeKeyAndVisible()
return true
```
1. Initialize the storyboard in code using the storyboard name.

2. Create a reference to the storyboard’s initial view controller.

3. Set the app delegate’s window using the device’s screen size as the frame.

4. Set the window’s root view controller to the storyboard’s initial view controller.

5. By calling makeKeyAndVisible() on your window, window is shown and positioned in front of every window in your app. For the most part, you’ll only need to work with one window. There are instances where you’d want to create new windows to display your app’s content. For example, you’ll work with multiple windows when you want to support an external display in your app.

# Launching a view controller without initializing storyboard
Open AppDelegate.swift.
Replace the existing code inside application(_:didFinishLaunchingWithOptions:) with the following:
```swift
let viewController = TabBarController()
window = UIWindow(frame: UIScreen.main.bounds)
window?.rootViewController = viewController
window?.makeKeyAndVisible()
return true
```

Build and run, and you’ll see a tab bar controller with a black background.
![image](https://user-images.githubusercontent.com/47273077/204135424-542cf9ca-e3c7-4a29-b070-ce5b3a3da2cd.png)
When you add a view controller onto a storyboard, the background view is set to white by default. 
In code, the view controller’s view has a nil background color, which shows up as black. 

## Building out a view controller’s user interface in code
```swift
import UIKit

final class ProfileHeaderView: UIView {
  override init(frame: CGRect) {
    super.init(frame: frame)
    backgroundColor = .groupTableViewBackground
  }
  
  required init?(coder aDecoder: NSCoder) {
    super.init(coder: aDecoder)
  }
}
```
With the code above, you override init(frame:). The method you’ve overridden is an initializer method. As the method name implies, this is where you add your initialization code, such as setting the view’s background color.

Afterward, init(coder:) takes care of the object’s archiving and unarchiving processes for Interface Builder. This method is handy when you launch an object from storyboard/.xib and want to configure the object at the initialization phase. Generally, when a view is created in code, init(frame:) is the initializer used, and when a view is created from a storyboard or .xib, init(coder:) is used instead.

# Refactoring stack views
```swift
private func setupStackView() {
  // 1
  addSubview(stackView)
  stackView.translatesAutoresizingMaskIntoConstraints = false
  
  // 2
  NSLayoutConstraint.activate(
    [stackView.centerXAnchor.constraint(equalTo: centerXAnchor),
     stackView.leadingAnchor.constraint(
      greaterThanOrEqualTo: leadingAnchor, constant: 20),
     stackView.leadingAnchor.constraint(
      lessThanOrEqualTo: leadingAnchor, constant: 500),
     stackView.bottomAnchor.constraint(
      equalTo: bottomAnchor, constant: -8),
     stackView.topAnchor.constraint(
      equalTo: topAnchor, constant: 26),
     
     profileImageView.widthAnchor.constraint(
      equalToConstant: 120),
     profileImageView.widthAnchor.constraint(
      equalTo: profileImageView.heightAnchor),
     
     leftSpacerView.widthAnchor.constraint(
      equalTo: rightSpacerView.widthAnchor)
    ])
  
  // 3
  profileImageView.setContentHuggingPriority(
    UILayoutPriority(251), 
    for: NSLayoutConstraint.Axis.horizontal)
  profileImageView.setContentHuggingPriority(
    UILayoutPriority(251),
    for: NSLayoutConstraint.Axis.vertical)
  
  fullNameLabel.setContentHuggingPriority(
    UILayoutPriority(251),
    for: NSLayoutConstraint.Axis.horizontal)
  fullNameLabel.setContentHuggingPriority(
    UILayoutPriority(251),
    for: NSLayoutConstraint.Axis.vertical)
  fullNameLabel.setContentCompressionResistancePriority(
    UILayoutPriority(751),
    for: NSLayoutConstraint.Axis.vertical)
  
  messageButton.setContentCompressionResistancePriority(
    UILayoutPriority(751),
    for: NSLayoutConstraint.Axis.horizontal)
}

```

3. Set the content hugging priority and compression resistance priority on profileImageView, fullNameLabel and messageButton to match the layout behavior from the Interface Builder implementation.

![image](https://user-images.githubusercontent.com/47273077/204136889-f736d75f-a01b-470e-88ea-3665867e3958.png)

-----
### Here are five benefits of using code to construct Auto Layout constraints:

* Everything technical that storyboard can do, code can do too. But, not vice versa.

* Readable merge conflict(s) means less time spent fixing merge conflicts.

* Code compilation time reduction.

* All the user interface logic lives in code. This benefit mitigates events such as having to find whether a property is changed in Interface Builder or code.

* Easy UI maintenance with the right coding infrastructure. Manage UI constants such as fonts, colors and constraint values with ease.

### Here are five drawbacks of using code:

* Higher learning curve compared to using Interface Builder.

* Naming conventions and code cleanliness are vital for code maintenance when working on a team.

* Inability to add user interface objects and create constraints for the user interface objects visually like in Interface Builder.

* More developers are familiar with using Interface Builder than developers who are familiar with using code to build an app’s layout. If you work with developers who are less familiar with using code, more time may be needed to properly onboard the developers.

* Opportunity cost of missing out some of the automation Interface Builder provides when you build your layouts in Interface Builder.


## Useful to use safeAreaLayoutGuide
```swift
    let contentLayoutGuide = view.safeAreaLayoutGuide
    
    NSLayoutConstraint.activate([
      mainStackView.leadingAnchor.constraint(equalTo:
        contentLayoutGuide.leadingAnchor),
      mainStackView.trailingAnchor.constraint(equalTo:
        contentLayoutGuide.trailingAnchor),
      mainStackView.topAnchor.constraint(equalTo:
        contentLayoutGuide.topAnchor),
    ])
````

## Setting up the scroll view

```swift

  private func setupMainStackView() {
    mainStackView.axis = .vertical
    mainStackView.distribution = .equalSpacing
    mainStackView.translatesAutoresizingMaskIntoConstraints
      = false
    
    //1
    scrollView.addSubview(mainStackView)
    
    //2
    let contentLayoutGuide = scrollView.contentLayoutGuide
    
    NSLayoutConstraint.activate([
      //3
      mainStackView.widthAnchor.constraint(equalTo:
        view.widthAnchor),
      mainStackView.leadingAnchor.constraint(equalTo:
        contentLayoutGuide.leadingAnchor),
      mainStackView.trailingAnchor.constraint(equalTo:
        contentLayoutGuide.trailingAnchor),
      mainStackView.topAnchor.constraint(equalTo:
        contentLayoutGuide.topAnchor),
      //4
      mainStackView.bottomAnchor.constraint(equalTo:
        contentLayoutGuide.bottomAnchor)
    ])
    
    //5
    setupProfileHeaderView()
    setupButtons()
  }
  
  private func setupScrollView() {
    //1
    scrollView.translatesAutoresizingMaskIntoConstraints = false
    view.addSubview(scrollView)

    let frameLayoutGuide = scrollView.frameLayoutGuide
      
    //2
    NSLayoutConstraint.activate([
      frameLayoutGuide.leadingAnchor.constraint(equalTo:
        view.leadingAnchor),
      frameLayoutGuide.trailingAnchor.constraint(equalTo:
        view.trailingAnchor),
     frameLayoutGuide.topAnchor.constraint(equalTo:
        view.safeAreaLayoutGuide.topAnchor),
      frameLayoutGuide.bottomAnchor.constraint(equalTo:
        view.safeAreaLayoutGuide.bottomAnchor)
    ])
  }

```
