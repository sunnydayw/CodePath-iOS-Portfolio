# iOS Topic Questions

## Views

#####   What properties of a view can be animated?
    Frame, bounds, center, Transformation, alpha, background color, contentStretch
    
#####   What is the difference between frame and bounds?
    Frame change size and position relative to superview. 
    Bounds change the it contents position and size relative to its own coordinate system.  

#####	How are the typical values used for RGB different than the values used when creating a CGColor (using RGB parameters) and how do you account for this?
	You have to give CG Color values between 0 and 1.0 So divide the RGB values by 255.

#####	What view property must be true in order for gesture recognizers to work?
	`userInteractionEnabled = true`

#####	Give 1-2 examples of when it'd be a good idea to build a custom view.
	When you have an elements that you going to reuse throughout the app that has specific layout style, or a custom behavior 

#####	When you want to separate the view from the view controller
	you want to separate the view when it is reuse the same view in serveral place or doing custom drawing, Also if subclassing would improve code legibility

##	Classes
#####	What does it mean when a class subclasses another class?
	When a class subclasses another class,  the subclass has the properties of the class it’s subclassing in addition to its properties. The class that was subclassed does not have properties of the subclass.

#####	Value Types
	Let vs Var

#####	Give an example of when we would use “type casting”.
	We have to type cast Int to a string for UILabel
	```
	Let number  = 5
	UILabel.Text = String(number)
	```

#####	Why is casting a UIView to a UIImageView considered “down casting”
	Because UiImageView is a subclass of UIView

##	View Controllers
#####	What are the view controller lifecycle methods?
	viewDidLoad -> viewDidAppear -> viewDidDisappear 

#####	What is the difference between viewDidLoad & viewDidAppear?
	viewDidLoad is called when the app is in memory whereas viewDidAppear gets called when the app is visible.

#####	When adding a child view controller to a container view controller, what are the view controller lifecycle methods you need to call on the child view controller? What about when removing?
	adding child view
	```
	addChildViewController(activeVC)
	activeVC.view.frame = contentView.bounds
	contentView.addSubview(activeVC.view)
	activeVC.didMoveToParentViewController(self)
	```
	Removing child view
	```
	inActiveVC.willMoveToParentViewController(nil)
    inActiveVC.view.removeFromSuperview()
    inActiveVC.removeFromParentViewController()
	```

#####	What is a container view controller? When is it useful?
	Container view controllers are a way to combine the content from multiple view controllers into a single user interface. It is useful to reuse the view controller.

#####	When should you add a new View Controller to your app?
	When a view have a difference function from anything other view.


##	Navigation
#####	What method do we use to pass data to another view controller that we are navigating to?
	prepareForSegue

#####	How do we pass data back when we are returning from another view controller?
	Protocol & delegate

#####	What use cases are best suited for show (push) navigation?
	Showing details, able to navigate back quickly 

#####	What must we include any time we want to use show (push) navigation?
	UInavigationController

#####	What use cases are best suited for modal presentation?
	When you want to present information quickly and remove quickly 

#####	When would you want to use a custom view controller transition?
	When you designer tells you too?
	
##	Optionals
#####	What is a Swift optional and how is it notated?
	is a variable that can hold either a value or no value
	`optional(“optional things here”)`

#####	Why is force unwrapping optionals dangerous?
	You might unwrapping a nil and crash the app

#####	What is optional chaining and when / why would you use this technique?
	You specify optional chaining by placing a question mark (?) If the optional contains a value, call success, if optional is nil it return nil
	Multiple queries can be chained together. If any link in the chain is nil, the entire chain fails gracefully with out crashing the app

##	Storyboard connections
#####	What is an outlet and when is it used?
	An outlet allows us to connect the user interface to the code. It’s used to modify the view elements to have specific values. 

#####	What is an Action and when is it used? Or What is target-action and when is it used?
		An action allows us to create user interaction when an element of the UI is manipulated or tapped by the user. 

#####	When creating Actions and Outlets, why is it advisable to drag from the document outline rather than from within the View Controller in the Storyboard?
	It is recc to drag from the document outline to prevent accidentally making an outlet or action an incorrect element on the storyboard 

#####	How do we associate a Swift File with a View Controller in the Storyboard?
	You can associate a swift file with a view controller in the identity inspector by setting the class.

##	Debugging
#####	When you run into the exception ... this class is not key value coding-compliant for the key ..., what is the first thing to check?
	When the outlet connection is missing or incorrect

#####	List at least 2 different reasons why you might encounter the error, “unexpectedly found nil while unwrapping an optional value ”, and explain how you might go about debugging this error?
	1.Forced unwrapping a variable and it’s nil (empty) 
	2.Accessing a preoperty that is nil e.g. textField.text
	You would debug this by tracing where the data inside of the variable is being retrieved from or by using breakpoint or Print.

##	Scroll Views, Table Views Collection Views
#####	When using a UIScrollView, which method in UIScrollViewDelegate would you use to detect when UIScrollView has finished scrolling.
	```
	optional func scrollViewDidEndDragging(_ scrollView: UIScrollView, willDecelerate decelerate: Bool)
	optional func scrollViewDidEndDecelerating(_ scrollView: UIScrollView)
	```
	scrollViewDidEndDragging and scrollViewDidEndDecelerating. 
	The first one is always called after the user lifts their finger. 
	If they scrolled fast enough to result in deceleration, `willDecelerate` will be `YES` 
	and the second method will be called after deceleration completes.

#####	How might you figure out if the user had scrolled to the bottom of a scroll view?
	if (scrollOffset + scrollViewHeight == scrollContentSizeHeight)

#####	What is cell recycling and why is it important?
	Cell recycling is the reuse of cells as the user scrolls through a UITableView. This helps us manage the phone memory, by not making all the cells. 

#####	How does the Table View know which prototype cell to reuse?
	```
	let cell = tableView.dequeueReusableCellWithIdentifier("Cel_Identifierl", forIndexPath: indexPath) as! Cell
	```

#####	How do we access properties in our custom cell class from within the cellForRowAtIndexPath method?
	Set the cell element to the corresponding element in the prototype cell.

#####	Where does all the logic associated with a particular cell go?
	All logic associated with cell  go into the custom cell class that you created.

#####	Why do we avoid naming Image Views and Labels we create in a prototype cell, “imageView” and “label” respectively?
		imageView and label is used by xcode, we shouldn't name it the same otherwise it will confuse the Xcode

#####	What is a protocol?
	A protocol is a blueprint of methods that must be run when the certain functionality needs to be used.

#####	What is UITableViewDataSource and when do you use it?
	UITableViewDataSource provides the table-view object with the information it needs to construct and modify a table view. You need it when you construct the tabelview

#####	What is UITableViewDelegate and when do you implement it?
	The UITableViewDelegate has certain optional functions that can be used with a table view if necessary. You would implement it when you use a table view in your project. 

#####	In which situations is it useful to use a CollectionView vs a TableView?
	When you need customized cells size.

#####	If you have an image-intensive iPhone app and want to decrease the lag time when loading images from disk or going through the network, what are some potential approaches to solving this issue?
	You can load in a lower resolution first and then load in a higher resolution photo that will replace the lower resolution image.

##	Cocoa Pods
#####	What are Cocoa Pods? What's an example of when it can be helpful to use a pod?
	CocoaPods is basicly a third party open-source libraries that you can include in your project and use it’s function. And it can help you scale your projects elegantly

#####	What are the advantages/disadvantages to including Pods in your gitignore file?
	An advantage of having the Pods in your gitignore is the source control repo will be smaller and take up less space. Also There won't be any conflicts to deal with when performing source control operations, such as merging branches with different Pod versions. A disadvantage is The Pod artifacts are guaranteed to be identical to those in the original installation after cloning the repo

##	App Architecture
#####	Describe the differing responsibilities of each component of the Model-View-Controller design pattern.
	The view controller's responsibility is to load and configure a view as well as ensure any navigation is handled appropriately. 
	View The objects that are in charge of the visual representation of the Model and the controls the user can interact with
	Model The object that holds your application data and defines how to manipulate it. It transforms the data into more presentable values
#####	Provide an example of MVC implementation.
	When user interact with the app, pulling to end of scrollview, View send the user action to the controller to request more data and the Model notifies the Controller of any data changes,and in turn, the Controller updates the data in the Views. 

#####	What's a singleton? Give an example of when you would want to use it. Or Describe a use case where using a shared instance make the most sense?
	A singleton is an object which is instantiated exactly once. Only one copy of this object exists and the state is shared and reachable by any other object.
Singleton is use when you want to share an instance, like in the Yelp app we create a shared instance user across the APIClient 

##	Auto Layout
#####	What is the difference between Auto Layout and Auto Resizing in iOS?
	Autoresizing is a matter of conceptually assigning a subview “springs and struts.” You can specify (using internal springs and struts) whether and how the view can be resized, and (using external springs and struts) whether and how the view can be repositioned.
	Autolayout, depends on the constraints of views.it’s a full-fledged object with numeric values, and can describe a relationship between any two views (not just a subview and its superview).

#####	What is the difference between content hugging priority & content compression resistance priority?
	Hugging => content does not want to grow
	Compression Resistance => content does not want to shrink

#####	What is intrinsic content size?
	intrinsic content size, which describes the minimum space needed to express the full view content without squeezing or clipping that data. 
	For an image view, for example, the intrinsic content size corresponds to the size of the image it presents.

#####	How would you animate views with AutoLayout?
	Animate changing the relative priorities view constraints

##	APIs
#####	What does OAuth allow for?
	Third Party authorization

#####	When would you want to use Parse?
	We use Parse when we need share data across different platform

#####	What data type to we typically get back from APIs?
	JSON

#####	What method can we use to dig into nested dictionaries?
	data serialization

##	General Application
#####	What does the NSUserDefaults class provide to you as the app developer?
	NSUserDefaults can persiste date accross app restart 

#####	List & explain the different types of iOS Application States.
	When an app starts, it transitions the Inactive state. It's actually running, but it's performing other functions and isn't ready to accept user input or events.

	An app in an Active state is running in the foreground and receiving events. This is the normal mode for foreground apps — apps that don’t have to run in the background without a user interface.

	When an app is in the Background state, its user interface isn't visible, but it is running. Most apps transition through this state on their way to being suspended.

	When an app is in the Not Running state, either the app hasn't been launched or the system shut it down.

#####	What is the very first method that is called when an app launches and what file is it found in?
	AppDelegate, didFinishLaunchingWithOptions function

##	Closures
#####	What is a closure?
	Closure are the blocks that can be passed around and used in our code

#####	How are closures helpful when passing data obtained from a network request?
	Closures can pass data from the API Client to current Viewcontroller so we dont need the whole API code in our viewcontroller

#####	Why do we need to use “self” inside the body of closures?
	We need to use self to reference instance to the Viewcontoller

#####	Why does the UIView.animateWithDuration method utilize a closure?
	It need to know when it finish the animaiton and to continues 

##	Design
#####	What are 1-2 examples of a good use of animation in some of the apps you use?
	Flopboard like how it animated the flow of the app
	Starbucks nice animation on the reward page, with star inside the cup & user interaction

#####	When would you use AVFoundation instead of UIImagePickerController?
	When we want considerably more control over how the camera is configured. to eliminate/config the iris, have a faster start and faster capture. 

#####	Choose an app that you use often and figure out all the different ways it leverages the device frameworks (i.e. camera, push notifications, maps, location, etc).
	Snapchat able to app animation while recording, changing sound effect.

#####	What's the difference between using storyboards, xib's, and programmatic views in your app? What are the pros and cons of each one?
	iOS Storyboards: A visual tool for laying out multiple application views and the transitions between them.
	Pro: Performance, Prototypes Con: Reusability, Data flow
	xib file corresponds to a single view element and can be laid out in the Interface Builder, making it a visual tool as well
	Pro: Reusability,Performance Con: Performance
	Custom Code: i.e., no GUI tools, but rather, handling all custom positioning, animation, etc. programmatically.
	Pro: Under the Hood, Reusability, Merge Conflicts Con: Prototyping, Refactoring

##	Networking
#####	What is the difference between NSURLConnection and NSURLSession?
	The NSURLConnection class provides convenience class methods to load URL requests both asynchronously using a callback block and synchronously.

	The NSURLSession provide an API for downloading content. It supporting authentication and gives your app the ability to perform background downloads when your app is not running.

#####	Now that there is NSURLSession, do we still need AFNetworking? Why or why not?
	One of the benefits of using AFNetworking is the data type classes for handling response data. Using AFJSONRequestOperation the success block has already parsed the response and returns the data for you. With NSURLSession you receive NSData back in the completion handler, so you would need to convert the NSData into JSON or other formats.

