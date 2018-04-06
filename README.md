# LogFile

Sample Log file in Markdown that I use to track my progress, using [MultiMarkdown Composer](http://multimarkdown.com/composer4/) 

Here's a sample of my Log.md file that I keep track of daily tasks, ideas, questions, issues, and code samples.

I don't always know what I'm doing, but this gives me a reference point if I need to re-visit something and I can quickly search for a solution that I previously used, or I can take some of the concepts and turn them into a blog post to share online.

There are typos, and errors, but that's ok, because it's a scratchpad of my day.

February 17 2018 12:02:00

## Custom Table View Cell ##

* Make sure you use the `contentView.layoutMarginsGuide` not `layoutMarginsGuide` ... they are different and the first works, the second doesn't ... because the cell will have a zero size ... 
* You can't set the contentView to translatesAutoresizingMaskIntoConstraints to false!
* Accidentally setting a constraint equal to another
* Need to think about what views will be driving the overall height (multipole line labels)
* Need to think about the constraints relative ... can't use the bottom constraint to equal to system spacing


## When Working With the Anchors ##

The constraintEqualToSystemSpacingBelow() is meant for constraints from top to bottom (not bottom to top)
The constraintEqualToSystemSpacingAfter() is meant for constraints from leading to trailing (not trailing to leading!)

NOTE: Setting up either of these incorrectly will mess up your layout, and you'll see that the views are overlapping on the edge right edge, or the bottom edge, since it'll do the opposite 8 point constant value


* Error if you don’t have same hierarchy
	* `UIViewLayoutMarginsGuide'.leading"> because they have no common ancestor.  Does the constraint or its anchors reference items in different view hierarchies?  That's illegal.'`

February 18 2018 22:44:00

## When to Use Compression Auto Layout ##

`H:|-[timeLabel]-8-[actionLabel]-8-[supplyLabel]-|`
`H:|-[noteLabel]-|`
`V:|-[actionLabel]-[noteLabel]-|`


## Error When Trying to Invert a Constraint ##


    actionLabel.bottomAnchor.constraintEqualToSystemSpacingBelow(noteLabel.topAnchor, multiplier: -1.0).isActive = true

Results in the Error:

	[LayoutConstraints] Could not resolve symbolic constant for constraint, because: Aligning the bottom edge of a UILabel with the top edge of a UILabel is not recommended. Use an explicit constant for your constraint to override this.

## Don't Use addConstraints() ??? ##


It won't add the correct constraints .. and you may get ambiguous layout warnings with your constraints ... or no height with your tableview cells

		 [Warning] Warning once only: Detected a case where constraints ambiguously suggest a height of zero for a tableview cell's content view. We're considering the collapse unintentional and using standard height instead.

ERROR:

		// BAD!!! ... addConstraints() should not be used on iOS 8+!!!!
        addConstraints(visualConstraints("H:|-[v0]-[v1]-[v2]-|", views: timeLabel, actionLabel, supplyLabel))
        addConstraints(visualConstraints("H:|-[v0]-|", views: noteLabel))
        addConstraints(visualConstraints("V:|-[v0]-[v1]-|", views: actionLabel, noteLabel))

CORRECT:

        addVisualConstraints("H:|-[v0]-[v1]-[v2]-|", views: timeLabel, actionLabel, supplyLabel)
        addVisualConstraints("H:|-[v0]-|", views: noteLabel)
        addVisualConstraints("V:|-[v0]-[v1]-|", views: actionLabel, noteLabel)


## Auto Layout Extension ##

	extension UIView {
	    func addVisualConstraints(_ visualConstraint: String, views: UIView ...) {
	        var viewDictionary = [String: UIView]()
	        for (index, view) in views.enumerated() {
	            viewDictionary["v\(index)"] = view
	            view.translatesAutoresizingMaskIntoConstraints = false
	        }
	        // Apple recommends to use the Activate method, to add to correct views
	        NSLayoutConstraint.activate(NSLayoutConstraint.constraints(withVisualFormat: visualConstraint, 
	        	options: NSLayoutFormatOptions(), metrics: nil, views: viewDictionary))
	    }
	}

## Auto Layout Visual Format

    // |-[v0]  will give the the margin
	// |-8-[v0] will give exact spacing


# Auto Layout Notes #

* Anchor API will give you compile type constraint checking
	* Prevents you from creating invalid constraints
* Using the visual format or the NSConstraint API will give Runtime checking, 
* Visual format language


February 19 2018 12:18:15

* Researching Auto Layout
	* <http://www.thinkandbuild.it/learn-to-love-auto-layout-programmatically/>
	* <https://www.hackingwithswift.com/read/6/3/auto-layout-in-code-addconstraints-with-visual-format-language>
	* <https://www.raywenderlich.com/174078/auto-layout-visual-format-language-tutorial-2>
* Fonts monospacing font: <https://stackoverflow.com/questions/38148073/uifont-monospaceddigitsystemfontofsize-not-really-monospaced>

February 19 2018 13:01:20

* Recording videos on Auto Layout

February 20 2018 10:35:34

* Recording videos on Auto Layout

February 21 2018 10:22:14

* Planning out work, and prepping next sprint for timer app


February 21 2018 10:47:51

* Timer planning

Reseting a Time Based Timer
* Should not reset to "duration" it should reset to the "next day" 
	* 10:45am, set for 10:46am ... counts down 60, 59... 00:00 > reset = 23:59 ...
	* Reset button should disable for timeBased "alarms"

February 22 2018 10:00:37

* Planned a meeting with Brad
* Worked with Erik on setting up timer text label code sample to use a monospaced digital font (Doesn't work with text AM/PM)

February 22 2018 12:25:24

* Reviewed tasks on Manuscript
* Code Review of flash-00 branch, looks good, much better state
	* Needs to have develop merged into it, since there are conflicts
	* Need to QA the final merge for next version of the timer app

February 22 2018 12:26:17

* Then I need to film a video on animating constraints
* Wrote for 10 minutes on blog topic (beta testing journey)

February 22 2018 12:44:36

* working on code sample for RIT class today, since I didn't do a good job preparing for class  

February 22 2018 14:33:22

* Dependency Injection Resources
	* [Nuts and Bolts of Dependency Injection in Swift](https://cocoacasts.com/nuts-and-bolts-of-dependency-injection-in-swift/)
	* [Dependency Injection Demystified](http://www.jamesshore.com/Blog/Dependency-Injection-Demystified.html)
	* [Dependency Injection with Storyboards](http://cleanswifter.com/dependency-injection-with-storyboards/)
	* [Swift Dependency Injection for View Controllers](https://www.theboffinlab.com/lab-notes/swift-dependency-injection-view-controllers)

February 23 2018 16:27:09

* Wrote blog post on beta testing
* Spoke with BrewJacket
* 5.12 Auto Layout Button - End
* Recorded 5 videos
	* Auto Layout Animation (Storyboard + Code)
	* Challenge Calculator UI


February 24 2018 09:18:56

* Listened to Swift by Sundell
	* Sommer Paige
	* Chris Edof

February 24 2018 10:06:31

* Trying to debug the mono space font
	* Small ui needs to be not centered, but based on the width, label should expand to fill.
	* There's a lot of calls to resize label, why?
		* 2 views setup?
* Content hugging/squishing???
	* 251, 750
* Content compression
	* 750, 750
* Changed the content compression to 250, 250 for the text to fix issues with auto layout changing window size when not centering


February 24 2018 14:14:15

* Working on the timer app

# Timer Run Loops #

Most of the time you create a simple timer, it'll just work.

But you're going to run into situations on iOS or on macOS where the timer will stop firing.

Your method to update the UI won't be called and that's because your timer is on the default run loop.

In order to get around this issue, you need to make sure that you manually add the timer to the right run loop mode.

Instead of using this logic to create the timer:

Use this logic so that it will update all the time.

On macOS, you'll see that the update block will fire every second, even when you resize the window.

On iOS, you'll see that your timer will update even when you're multitasking or receiving a phone call.


Done: Merge in changes from the flashing logic FLASH-00, and then prep a new build to send to beta testers


February 24 2018 14:17:00

## Super Easy Timer notes

* Update theme code

February 26 2018 12:49:57

* Playing with ThemeKit, trying to get the app stylized using the new style


## Working With Attributed Strings in Swift 4 ##


* <https://stackoverflow.com/a/32269975/276626>

		let myString = "Swift Attributed String"
		let myAttribute = [ NSAttributedStringKey.foregroundColor: UIColor.blue ]
		let myAttrString = NSAttributedString(string: myString, attributes: myAttribute) 
		
		// set attributed text on a UILabel
		myLabel.attributedText = myAttrString




# Submitting a New App to the App Store #

Bundle Identifier:
1. Create a Mac App ID: <https://developer.apple.com/account/mac/identifier/bundle>
2. Wait for Apple to propagate changes, and then use it
3. Your BundleId needs to match in Xcode

SKU: SuperEasyTimer


February 27 2018 15:23:25

* Updated app icon
* Merged in changes on Super Easy Apps

## Making a NSTextField (Label) Center and Word Wrap? ##

* I don't know how to make it word wrap, since it doesn't do that unless I drag out multiple lines...
	* Not sure why it doesn't work
* To center it, and prevent the lines from being long, I need to add two constraints to either side.
	* In macOS it seems to be a bit more picky, when I just want the label to fill the available space.
	* Workaround seems to just be to make it taller ... otherwise we might need code, since the features don't seem to work like on iOS

March 1 2018 12:12:07

* Working on icon designs for Super Easy Timer
	* Lines need to be converted to outlines to combine them with shapes
	* Lines allow you to alias to create the exact matchup, while a shape will be stuck on the actual grid lines
* Borders are needed to keep symbols a uniform size, so that you can use them in your design
	* And this makes it much easier to export, since they are all consistent
	* Add it to set the minimum size, and then you can place the icons where you expect, and they can take the space you expect them to take

March 1 2018 16:38:41

* Xcode project rename doesn't work, you have ot manually rename the file, otherwise you get the error that it can't build your project

March 2 2018 15:21:28

* Playing with the Coding protocol and Swift
* Attempting to use the Codable interface in Swift 4 with a simple person class object (it does't work with enum values)

# 1st Error

	class Person: Codable { 
	    var name: String = "Paul"
	    var age: Int = 31
	    
	    init(name: String, age: Int) {
	        self.name = name
	        self.age = age
	    }
	}

Buggy Code:

    func archive() {
        let person = Person(name: "Dave", age: 33)
        let data = NSKeyedArchiver.archivedData(withRootObject: person)
        let newPerson = NSKeyedUnarchiver.unarchiveObject(with: data)
        print("New Person")
    }

Error: 

	2018-03-02 15:23:22.585430-0500 TestCodable[97310:4802222] *** NSForwarding: warning: object 0x60800005a370 of class 'TestCodable.Person' does not implement methodSignatureForSelector: -- trouble ahead
	Unrecognized selector -[TestCodable.Person replacementObjectForKeyedArchiver:]
	2018-03-02 15:23:22.586008-0500 TestCodable[97310:4802222] Unrecognized selector -[TestCodable.Person replacementObjectForKeyedArchiver:]
	(lldb) 

# 2nd Error: 

Hint to use NSObject subclass, since it's part of the Objective-C NSCoding requirement. <https://stackoverflow.com/questions/25805599/got-unrecognized-selector-replacementobjectforkeyedarchiver-crash-when-impleme>

Changed to using NSObject subclass for NSKeyedArchiver class

	class Person: NSObject, Codable {
	    var name: String = "Paul"
	    var age: Int = 31
	    
	    init(name: String, age: Int) {
	        self.name = name
	        self.age = age
	    }
	}

Still no dice ... different error


	2018-03-02 15:20:57.092741-0500 TestCodable[97221:4798079] -[TestCodable.Person encodeWithCoder:]: unrecognized selector sent to instance 0x60400005ed80
	2018-03-02 15:20:57.098458-0500 TestCodable[97221:4798079] *** Terminating app due to uncaught exception 'NSInvalidArgumentException', reason: '-[TestCodable.Person encodeWithCoder:]: unrecognized selector sent to instance 0x60400005ed80'

#  Conform to NSCoding #

	class Person: NSObject, NSCoding {
	    func encode(with aCoder: NSCoder) {
	        aCoder.encode(name, forKey: "name")
	        aCoder.encode(age, forKey: "age")
	    }
	
	    required init?(coder aDecoder: NSCoder) {
	        self.name = aDecoder.decodeObject(forKey: "name") as! String
	        self.age = aDecoder.decodeInteger(forKey: "age")
	    }
	
	    var name: String = "Paul"
	    var age: Int = 31
	    
	    init(name: String, age: Int) {
	        self.name = name
	        self.age = age
	    }
	
	    override var description: String {
	        return "Name: \(name), age: \(age)"
	    }
	}

# Structs Don't work either with Coding and NSKeyedArchiver

	2018-03-02 15:40:03.158939-0500 TestCodable[97952:4830712] -[_SwiftValue encodeWithCoder:]: unrecognized selector sent to instance 0x60c00009b800
	2018-03-02 15:40:03.167011-0500 TestCodable[97952:4830712] *** Terminating app due to uncaught exception 'NSInvalidArgumentException', reason: '-[_SwiftValue encodeWithCoder:]: unrecognized selector sent to instance 0x60c00009b800'
	*** First throw call stack:


