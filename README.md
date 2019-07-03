<p align="center">
    <a href="LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-brightgreen.svg" alt="MIT License">
    </a>
    <a href="https://swift.org">
        <img src="https://img.shields.io/badge/swift-4.2-brightgreen.svg" alt="Swift 4.2">
    </a>
    <a href="https://cocoapods.org/pods/UIKit-Plus">
        <img src="https://img.shields.io/cocoapods/v/UIKit-Plus.svg" alt="Cocoapod">
    </a>
</p>

**This project is in active development state and anything may change till 1.0.0**

Build UI in SwiftUI-like way right now in Xcode10+ and for iOS9 and higher! 😺

```swift
// NOTE:
// Now it's written for Swift 4.2-5.0
// but closer to 5.1 release it will support 5.1 features like `@State` and `@Binding`
// and became look more like SwiftUI cause `functionBuilder became available.
```

Support this lib by giving a ⭐️!

## Installation

#### With [CocoaPods](https://cocoapods.org)

Add the following line to your Podfile:
```ruby
pod 'UIKit+Plus', '~> 0.2.0'
```

#### With [Swift Package Manager](https://swift.org/package-manager/)

In Xcode11 go to `File -> Swift Packages -> Add Package Dependency` and enter there URL of this repo
```
https://github.com/MihaelIsaev/UIKitPlus
```

#### With [Carthage](https://github.com/Carthage/Carthage)

Not supported yet. Feel free to send PR for that.

## Usage

```swift
import UIKit
import UIKitPlus
```

### Cheatsheet
| UIKitPlus  | UIKit |
| ------- | -------------- |
| View | UIView |
| WrapperView | UIView |
| ScrollView | UIScrollView |
| CollectionView | UICollectionView |
| TableView | UITableView |
| Image | UIImageView |
| Button | UIButton |
| Label | UILabel |
| TextField | UITextField |
| StackView | UIStackView |
| HStackView |  |
| VStackView |  |
| VerificationCodeView |  |

### View
It is jsut simple view
```swift
View().background(.red).shadow()
```

### WrapperView
It is simple `View` but with ability to initialize with inner view
```swift
WrapperView {
  View().background(.red).shadow()
}.background(.green).shadow()
```
and you could specify innerView`s padding right here
```swift
// to the same padding for all sides
WrapperView {
  View()
}.padding(10)
// or to specific padding for each side
WrapperView {
  View()
}.padding(top: 10, left: 5, right: 10, bottom: 5)
// or even like this
WrapperView {
  View()
}.padding(top: 10, right: 10)
```

### ScrollView
Nothing interesting yet, but you could specify some settings in declarative manner
```swift
ScrollView().paging(true).scrolling(false).hideIndicator(.horizontal)
ScrollView().paging(true).scrolling(false).hideAllIndicators()
ScrollView().contentInset(.zero)
ScrollView().contentInset(top: 10, left: 5, right: 5, bottom: 10)
ScrollView().contentInset(top: 10, bottom: 10)
ScrollView().scrollIndicatorInsets(.zero)
ScrollView().scrollIndicatorInsets(top: 10, left: 5, right: 5, bottom: 10)
ScrollView().scrollIndicatorInsets(top: 10, bottom: 10)
```

### CollectionView
Nothing interesting yet
```swift
CollectionView().paging(true)
```

### TableView
Nothing interesting yet

### Image
```swift
Image("someImage").mode(.scaleAspectFill).clipsToBounds(true)
```

### Button
```swift
Button()
Button("Tap me")
Button().title("Tap me") // useful if you declared Button from extension like below
Button.mySuperButton.title("Tap me")
```
background and background for highlighted state
```swift
Button("Tap me").background(.white).backgroundHighlighted(.darkGray)
```
title color for different states
```swift
Button("Tap me").color(.black).color(.lightGray, .disabled)
```
set some font from declared identifiers or with system fonts
```swift
Button("Tap me").font(v: .systemFont(ofSize: 15))
Button("Tap me").font(.sfProBold, 15)
```
add image
```swift
Button("Tap me").image(UIImage(named: "cat"))
Button("Tap me").image("cat")
```
You can handle tap action easily
```swift
Button("Tap me").tapAction { print("button tapped") }
```
or like this
```swift
func tapped() { print("button tapped") }
Button("Tap me").tapAction(tapped)
```

### Label
It either may be initialized with `String` or unlimited amount of `AttributedString`s
```swift
Label("hello 👋 ")
Label().text("hello") // useful if declare label in extension like below
Label.mySuperLabel.text("hello")
Label(AttributedString("hello").foreground(.red), AttributedString("world").foreground(.green))
```
set some font from declared identifiers or with system fonts
```swift
Label("hello").font(v: .systemFont(ofSize: 15))
Label("hello").font(.sfProBold, 15)
```
set text color
```swift
Label("hello").color(.red)
```
set text alignment
```swift
Label("hello").alignment(.center)
```
set amount of lines
```swift
Label("hello").lines(1)
Label("hello\nworld").lines(0)
Label("hello\nworld").lines(2)
Label("hello\nworld").multiline()
```

### TextField
```swift
TextField()
TextField("some text")
TextField().text("some text")
TextField.mySuperDuperTextField.text("some text")
```
set some font from declared identifiers or with system fonts
```swift
TextField().font(v: .systemFont(ofSize: 15))
TextField().font(.sfProBold, 15)
```
set text color
```swift
TextField().color(.red)
```
set text alignment
```swift
TextField().alignment(.center)
```
placeholder
```swift
TextField().placeholder("email")
// or use AttributedString to make it colored
TextField().placeholder(AttributedString("email").foreground(.green))
```
secure
```swift
TextField().secure()
```
remove any text from field easily
```swift
TextField().cleanup()
```
set keyboard and content type
```swift
TextField().keyboard(.emailAddress).content(.emailAddress)
```
set delegate
```swift
TextField().delegate(self)
```
or get needed events declarative way
```swift
TextField().shouldBeginEditing { tf in return true }
           .didBeginEditing { tf in }
           .shouldEndEditing { tf in return true }
           .didEndEditing { tf in }
           .shouldChangeCharacters { tf, range, replacement in return true }
           .shouldClear { tf in return true }
           .shouldReturn { tf in return true }
           .editingDidBegin { tf in }
           .editingChanged { tf in }
           .editingDidEnd { tf in }
```

### StackView
```swift
StackView().axis(.vertical)
           .alignment(.fill)
           .distribution(.fillEqually)
           .spacing(16)
```

### HStackView
The same as `StackView` but with predefined axis and ability to easily add arranged subviews
```swift
HStackView (
  Label("hello world").background(.green),
  Label("hello world").background(.red)
).spacing(10)
```

### VStackView
The same as `StackView` but with predefined axis and ability to easily add arranged subviews
```swift
VStackView (
  Label("hello world").background(.green),
  Label("hello world").background(.red)
).spacing(10)
```

### VerificationCodeView
This is really bonus view! :D Almost every app now uses verification codes for login and now you can easily implement that code view with UIKitPlus! :)
```swift
VerificationCodeField().digitWidth(64)
                       .digitsMargin(25)
                       .digitBorder(.bottom, 1, 0xC6CBD3)
                       .digitColor(0x171A1D)
                       .font(.sfProRegular, 32)
                       .entered(verify)

func verify(_ code: String) {
  print("entered code: " + code)
}
```

### Any view

#### Background
```swift
View().background(.red)
View().background(0xff0000)
```

#### Tint
```swift
View().tint(.red)
View().tint(0xff0000)
```

#### Corners
To set radius to all corners
```swift
View().corners(10)
```
To set custom radius for specific corner
```swift
View().corners(10, .topLeft, topRight)
View().corners(10, .topLeft, .bottomRight)
View().corners(10, .topLeft, topRight, .bottomLeft, .bottomRight)
```
To make you view's corners round automatically by smaller side
```swift
View().circle()
```

#### Borders
To set border on all sides
```swift
View().border(1, .black)
View().border(1, 0x000)
```
To set border on specific side
```swift
View().border(.top, 1, .black)
View().border(.left, 1, .black)
View().border(.right, 1, .black)
View().border(.bottom, 1, .black)
```
To remove border from specific side
```swift
.removeBorder(.top)
```

#### Alpha
```swift
View().alpha(0)
```

#### Opacity
```swift
View().opacity(0)
```

#### Hidden
```swift
View().hidden() // true by default
View().hidden(true)
View().hidden(false)
```

#### Rasterize
To rasterize layer, e.g. for better shadow performance
```swift
View().rasterize() // true by default
View().rasterize(true)
View().rasterize(false)
```

#### Shadow
```swift
View().shadow() // by default it's black, opacity 1, zero offset, radius 10
View().shadow(.gray, opacity: 0.8, offset: .zero, radius: 5)
View().shadow(0x000000, opacity: 0.8, offset: .zero, radius: 5)
```

#### Shake
You can shake any view just by calling
```swift
View().shake()
```
And you could customize shake effect
```swift
View().shake(values: [-20, 20, -20, 20, -10, 10, -5, 5, 0],
             duration: 0.6,
             axis: .horizontal,
             timing: .easeInEaseOut)
View().shake(-20, 20, -20, 20, -10, 10, -5, 5, 0,
             duration: 0.6,
             axis: .horizontal,
             timing: .easeInEaseOut)
```
or even create an extension
```swift
import UIKitPlus

extension DeclarativeProtocol {
  func myShake() {
      View().shake(-20, 20, -20, 20, -10, 10, -5, 5, 0,
                   duration: 0.6,
                   axis: .horizontal,
                   timing: .easeInEaseOut)
  }
}
```

#### AttributedString
You could create attributed strings in declarative way easily
```swift
AttributedString("hello").background(.gray)
                         .foreground(.red)
                         .font(.sfProBold, 15)
                         .paragraphStyle(.default)
                         .ligature(1)
                         .kern(1)
                         .strikethroughStyle(1)
                         .underlineStyle(.patternDash)
                         .strokeColor(.purple)
                         .strokeWidth(1)
                         .shadow()
                   // or .shadow(offset: .zero, blur: 1, color: .lightGray)
                         .textEffect("someEffect")
                         .attachment(someAttachment)
                         .link("http://github.com")
                         .baselineOffset(1)
                         .underlineColor(.cyan)
                         .strikethroughColor(.magenta)
                         .obliqueness(1)
                         .expansion(1)
                         .glyphForm(.horizontal)
                         .writingDirection(.rightToLeft)
```

#### Constraints
##### Size
You can set view size by passing `width` and `height` values like this
```swift
View().size(100, 200)
```
or square size by passing single value
```swift
View().size(100)
```
or view's size can be equal to other view size so when you change size of one view other view will change its size as well
```swift
let view1 = View().size(100, 200)
let view2 = View().sameSize(as: view1)
```
Of course you can specify just width or just height or both but by separate methods
```swift
View().width(100)
View().height(200)
View().width(100).height(200)
```
##### Superview
Your view can stick to its superview by any side or even by all sides
```swift
// this way it will stick with 0 constant value
View().edgesToSuperview()
// this way it will stick with 10 constant value for all sides
View().edgesToSuperview(10)
// also you could specify some values manually, but all the rest values are 0 by default
View().edgesToSuperview(top: 16, leading: 16, trailing: -16)
View().edgesToSuperview(trailing: -16, bottom: -16)
```
you could stick your view to only one side of superview like this
```swift
// empty argument means 0 constant value
View()topToSuperview()
View()topToSuperview(16)
View()leadingToSuperview()
View()leadingToSuperview(16)
View()trailingToSuperview()
View()trailingToSuperview(16)
View()bottomToSuperview()
View()bottomToSuperview(16)
View()centerXToSuperview()
View()centerXToSuperview(16)
View()centerYToSuperview()
View()centerYToSuperview(16)
View()widthToSuperview()
View()heightToSuperview()
```
##### Relative
Any side of your view could also stick to any side of other view
```swift
View().top(to: otherView.bottomAnchor)
View().leading(to: otherView.trailingAnchor)
View().trailing(to: otherView.leadingAnchor)
View().bottom(to: otherView.topAnchor)
View().centerX(to: otherView.centerXAnchor)
View().centerY(to: otherView.centerYAnchor)
View().width(to: otherView.widthAnchor)
View().height(to: otherView.heightAnchor)
```
or this way
```swift
View().edge(.top, to: anotherView.bottomAnchor)
View().edge(.leading, to: anotherView.trailingAnchor)
View().edge(.trailing, to: anotherView.leadingAnchor)
View().edge(.bottom, to: anotherView.topAnchor)
View().edge(.centerX, to: anotherView.centerXAnchor)
View().edge(.centerY, to: anotherView.centerYAnchor)
View().edge(.width, to: anotherView.widthAnchor)
View().edge(.height, to: anotherView.heightAnchor)
```
##### Center
Your view could be in center of its superview
```swift
View().centerInSuperview() // exact center
View().centerInSuperview(10) // exact center +10 by x-axis, and +10 by y-axis
View().centerInSuperview(x: 5, y: 10) // exact center +5 by x-axis, and +10 by y-axis
```
also it may be in center of another view
```swift
View().center(in: anotherView) // exact center
View().center(in: anotherView, 10) // exact center +10 by x-axis, and +10 by y-axis
View().center(in: anotherView, x: 5, y: 10) // exact center +5 by x-axis, and +10 by y-axis
```

##### Links to constraints
You can reach any view's constraint just like this
```swift
let view = View().edgesToSuperview()
```
now your view have top, leading, trailing and bottom constraints to its superview and e.g. you want to change `top` constraint so you could do it like this
```swift
view.top = 16
```
or
```swift
view.constraints.top?.constant = 16
```
the same way works with all view's constraints, so you can change them or even delete them just by setting them `nil`.

##### SafeArea
You could get `safeArea` safely at any view without `#available(iOS 11.0, *)` check like this
```swift
someView.safeArea.topAnchor
```

##### Constraint values
Any constraint value may be set as just `CGFloat` or with `Relation` and even `Multiplier`
```swift
View().leading(to: anotherView, 10) // just equal to 10
View().leading(to: anotherView, >=10) // greaterThanOrEqual to 10
View().leading(to: anotherView, <=10) // lessThanOrEqual to 10
View().leading(to: anotherView, 10 * 1.5) // equal to 10 with 1.5 multiplier
View().leading(to: anotherView, 10 * 1.5 | 999) // equal to 10 with 1.5 multiplier and 999 priority
View().leading(to: anotherView, 10 * 1.5 | .defaultLow) // equal to 10 with 1.5 multiplier and `.defaultLow` priority
View().leading(to: anotherView, 10 | 999) // equal to 10 with 999 priority
```

### Colors
With UIKitPlus you're able to use hex colors just by typing them with `0x` prefix like `0x000` for black or `0xfff` for white.

### Extensions

#### Fonts
Add your custom fonts to the project and then declare them like this
```swift
import UIKitPlus

extension FontIdentifier {
    public static var sfProBold = FontIdentifier("SFProDisplay-Bold")
    public static var sfProRegular = FontIdentifier("SFProDisplay-Regular")
    public static var sfProMedium = FontIdentifier("SFProDisplay-Medium")
}
```
and then use them just like
```swift
Button().font(.sfProMedium, 15)
```

#### Colors
Declare custom colors like this
```swift
import UIKit
import UIKitPlus

extension UIColor {
    static var mainBlack: UIColor { return .black  }
    static var otherGreen: UIColor { return 0x3D7227.color  } // 61 114 39
}
```
and then use them just like
```swift
Label("Hello world").color(.otherGreen).background(.mainBlack)
```

#### Buttons
Declare custom buttons like this
```swift
import UIKitPlus

extension Button {
    static var bigBottomWhite: Button {
        return Button().color(.darkGray).color(.black, .highlighted).font(.sfProMedium, 15).background(.white).backgroundHighlighted(.lightGray).circle()
    }
    static var bigBottomGreen: Button {
        return Button().color(.white).font(.sfProMedium, 15).background(.mainGreen).circle()
    }
}
```
and then use them like this
```swift
Button.bigBottomWhite.size(300, 50).bottomToSuperview(20).centerInSuperview()
```

#### Labels
Declare custom attributed labels like this
```swift
import UIKitPlus

extension Label {
    static var welcomeLogo: Label {
        return .init(AttributedString("My").foreground(.white).font(.sfProBold, 26),
                     AttributedString("App").font(.sfProBold, 26))
    }
}
```
and then use them like this
```swift
let logo = Label.welcomeLogo.centerInSuperview()
```

#### Images
Declare asset images like this
```swift
import UIKitPlus

extension Image {
    static var welcomeBackground: Image { return Image("WelcomeBackground") }
}
```
and then use them like this
```swift
let backgroudImage = Image.welcomeBackground.edgesToSuperview()
```

#### Subviews
Add subviews in one line
```swift
view.addSubview(view1, view2, view3)
```