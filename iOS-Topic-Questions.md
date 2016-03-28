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

##	Classes
#####	What does it mean when a class subclasses another class?
#####	Value Types
#####	Give an example of when we would use “type casting”.
#####	Why is casting a UIView to a UIImageView considered “down casting”

##	View Controllers
#####	What are the view controller lifecycle methods?
#####	What is the difference between viewDidLoad & viewDidAppear?
#####	When adding a child view controller to a container view controller, what are the view controller lifecycle methods you need to call on the child view controller? What about when removing?
#####	What is a container view controller? When is it useful?
#####	When should you add a new View Controller to your app?

##	Navigation
#####	What method do we use to pass data to another view controller that we are navigating to?
#####	How do we pass data back when we are returning from another view controller?
#####	What use cases are best suited for show (push) navigation?
#####	What must we include any time we want to use show (push) navigation?
#####	What use cases are best suited for modal presentation?
#####	When would you want to use a custom view controller transition?

##	Optionals
#####	What is a Swift optional and how is it notated?
#####	Why is force unwrapping optionals dangerous?
#####	What is optional chaining and when / why would you use this technique?

##	Storyboard connections
#####	What is an outlet and when is it used?
#####	What is an Action and when is it used? Or What is target-action and when is it used?
#####	When creating Actions and Outlets, why is it advisable to drag from the document outline rather than from within the View Controller in the Storyboard?
#####	How do we associate a Swift File with a View Controller in the Storyboard?

##	Debugging
#####	When you run into the exception ... this class is not key value coding-compliant for the key ..., what is the first thing to check?
#####	List at least 2 different reasons why you might encounter the error, “unexpectedly found nil while unwrapping an optional value ”, and explain how you might go about debugging this error?

##	Scroll Views, Table Views Collection Views
#####	When using a UIScrollView, which method in UIScrollViewDelegate would you use to detect when UIScrollView has finished scrolling.
#####	How might you figure out if the user had scrolled to the bottom of a scroll view?
#####	What is cell recycling and why is it important?
#####	How does the Table View know which prototype cell to reuse?
#####	How do we access properties in our custom cell class from within the cellForRowAtIndexPath method?
#####	Where does all the logic associated with a particular cell go?
#####	Why do we avoid naming Image Views and Labels we create in a prototype cell, “imageView” and “label” respectively?
#####	What is a protocol?
#####	What is UITableViewDataSource and when do you use it?
#####	What is UITableViewDelegate and when do you implement it?
#####	In which situations is it useful to use a CollectionView vs a TableView?
#####	If you have an image-intensive iPhone app and want to decrease the lag time when loading images from disk or going through the network, what are some potential approaches to solving this issue?

##	Cocoa Pods
#####	What are Cocoa Pods? What's an example of when it can be helpful to use a pod?
#####	What are the advantages/disadvantages to including Pods in your gitignore file?

##	App Architecture
#####	Describe the differing responsibilities of each component of the Model-View-Controller design pattern.
#####	Provide an example of MVC implementation.
#####	What's a singleton? Give an example of when you would want to use it. Or Describe a use case where using a shared instance make the most sense?

##	Auto Layout
#####	What is the difference between Auto Layout and Auto Resizing in iOS?
#####	What is the difference between content hugging priority & content compression resistance priority?
#####	What is intrinsic content size?
#####	How would you animate views with AutoLayout?

##	APIs
#####	What does OAuth allow for?
#####	When would you want to use Parse?
#####	What data type to we typically get back from APIs?
#####	What method can we use to dig into nested dictionaries?

##	General Application
#####	What does the NSUserDefaults class provide to you as the app developer?
#####	List & explain the different types of iOS Application States.
#####	What is the very first method that is called when an app launches and what file is it found in?

##	Closures
#####	What is a closure?
#####	How are closures helpful when passing data obtained from a network request?
#####	Why do we need to use “self” inside the body of closures?
#####	Why does the UIView.animateWithDuration method utilize a closure?

##	Design
#####	What are 1-2 examples of a good use of animation in some of the apps you use?
#####	When would you use AVFoundation instead of UIImagePickerController?
#####	Choose an app that you use often and figure out all the different ways it leverages the device #####	frameworks (i.e. camera, push notifications, maps, location, etc).
#####	What's the difference between using storyboards, xib's, and programmatic views in your app? What are the pros and cons of each one?

##	Networking
#####	What is the difference between NSURLConnection and NSURLSession?
#####	Now that there is NSURLSession, do we still need AFNetworking? Why or why not?