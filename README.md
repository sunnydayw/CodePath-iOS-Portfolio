# CodePath iOS Portfolio
Time spent: **100+** hours spent in total Coding Swift Since December 20, 2015 - March 26, 2016
For Video Demo, Please Check Video Demo Profile

## Implemented Features
##### UI Elements

    1.TableView & Collection View
    2.Scroll View
    3.SearchBar
    4.Camera
    5.Map View
    6.AutoLayout
    7.Tab Controller 
    8.Navigation Controller

##### User Ineraction

    1.Pull and Refresh
    2.Infinite Scroll
    3.Gestures
    4.Pulling down the profile page should blur and resize the header image

##### Animation

    1.Animating multiple View properties - frame,alpha etc
    2.Animating view transform - rotation,scale etc
    3.Spring Animations
    4.Combining Animation

##### Backend

    1.Parse server - user login/logout
    2.user profiles
    3.Tweeter/Instagram like post 

##### Other

    1.OAuth
    2.CocoaPod
    3.Data Model
    4.View Model
    5.API Client
    6.NSNotificationCenter

## Code Sample

#### UI Elements:

- TableView
```
    // MARK: - TabelView
    extension TweetsViewController: UITableViewDelegate,UITableViewDataSource {
        
        func tableView(tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
            if let tweets = tweets {
                return tweets.count
            }else{
                return 0
            }
        }
        
        func tableView(tableView: UITableView, cellForRowAtIndexPath indexPath: NSIndexPath) -> UITableViewCell {
            let cell = tableView.dequeueReusableCellWithIdentifier("TweetCell", forIndexPath: indexPath) as! TweetCell
            if let tweets = tweets {
                cell.tweets = tweets[indexPath.row]
                cell.delegate = self
                if likeStates[indexPath.row] != nil {
                    if likeStates[indexPath.row] == false {
                        cell.likeButton.setImage(UIImage(named: "like-action"), forState: UIControlState.Normal)
                        cell.likeTap = false
                    } else {
                        cell.likeButton.setImage(UIImage(named: "like-action-on"), forState: UIControlState.Normal)
                        cell.likeTap = true
                    }
                }
                if retweetStates[indexPath.row] != nil {
                    if retweetStates[indexPath.row] == false {
                        cell.retweetButton.setImage(UIImage(named: "retweet-action"), forState: UIControlState.Normal)
                        cell.retweetTap = false
                    } else {
                        cell.retweetButton.setImage(UIImage(named: "retweet-action-on"), forState: UIControlState.Normal)
                        cell.retweetTap = true
                    }
                }
            }
            return cell
        }
```

- SearchBar
```
  // MARK: - Search Filter
  func filtersviewController(filtersViewController: FiltersViewController, didUpdateFilters filters: [String : AnyObject]) {
    let categories = filters["categories"] as? [String]
    Business.searchWithTerm(selectedCategiors,location: mylocation, sort: nil, categories: categories, deals: nil) { (businesses: [Business]!, error: NSError!) -> Void in
      if businesses != nil {
        self.businesses = businesses
      } else {
        self.businesses = []
        
      }
      self.tableView.reloadData()
    }
  }
```

- Camera
```
    class CameraViewController: UIViewController, UIImagePickerControllerDelegate, UINavigationControllerDelegate {

        let vc = UIImagePickerController()
        
        override func viewDidLoad() {
            super.viewDidLoad()
            vc.delegate = self
            vc.allowsEditing = true
        }

    func imagePickerController(picker: UIImagePickerController,
        didFinishPickingMediaWithInfo info: [String : AnyObject]) {
            // Get the image captured by the UIImagePickerController
            //let originalImage = info[UIImagePickerControllerOriginalImage] as! UIImage
            let editedImage = info[UIImagePickerControllerEditedImage] as! UIImage
            // Do something with the images (based on your use case)
            // Dismiss UIImagePickerController to go back to your original view controller
            dismissViewControllerAnimated(true, completion: nil)
            let storyboard = UIStoryboard(name:"Main", bundle: NSBundle.mainBundle())
            let newPostNav = storyboard.instantiateViewControllerWithIdentifier("NewPostNavigationController") as! UINavigationController
            let newPostVC = newPostNav.topViewController as! NewPostViewController
            newPostVC.newImg = editedImage
            presentViewController(newPostNav, animated: true, completion: nil)
    }
```

- Map View
```
 override func viewDidLoad() {
      super.viewDidLoad()
      locationManager = CLLocationManager()
      mapView.delegate = self
      locationManager.desiredAccuracy = kCLLocationAccuracyBest
      locationManager.distanceFilter = 200
      locationManager.requestWhenInUseAuthorization()
      // display current location
      /*
      // draw circular overlay centered in my coordinate
      let coordinate = CLLocationCoordinate2D(latitude: 37.7833, longitude: -122.4167)
      let circleOverlay: MKCircle = MKCircle(centerCoordinate: coordinate, radius: 1000)
      mapView.addOverlay(circleOverlay)
      // Start puting annotation for businesses
      */
      //let centerLocation = CLLocation(latitude: 37.7833, longitude: -122.4167)
      //goToLocation(myLocation!)
      Dispatch.async( delay: 0.5) { () -> () in
        if self.locationManager.location != nil {
          let lat = self.locationManager.location!.coordinate.latitude
          let lon = self.locationManager.location!.coordinate.longitude
          let myLocation = CLLocation(latitude: lat, longitude: lon)
          self.goToLocation(myLocation)
        }
      }
      
      for business in businesses {
      let businessLoaction = CLLocationCoordinate2D(latitude: business.coordinate.0!, longitude: business.coordinate.1!)
      let title = business.name! as String
      addAnnotationAtCoordinate(businessLoaction,title: title)
      }
      
    }
```


- Tab Controller
```
    window = UIWindow(frame: UIScreen.mainScreen().bounds)
    let storyboard = UIStoryboard(name: "Main", bundle: nil)

    let nowPlayingNavigationController = storyboard.instantiateViewControllerWithIdentifier("MoviesNavController") as! UINavigationController
    let nowPlayingViewController = nowPlayingNavigationController.topViewController as! MovieViewController
    nowPlayingViewController.endpoint = "now_playing"
    nowPlayingNavigationController.tabBarItem.title = "Now Playing"
    nowPlayingNavigationController.tabBarItem.image = UIImage(named: "now_playing")

    let topRatedNavigationController = storyboard.instantiateViewControllerWithIdentifier("MoviesNavController") as! UINavigationController
    let topRatedViewController = topRatedNavigationController.topViewController as! MovieViewController
    topRatedViewController.endpoint = "top_rated"
    topRatedNavigationController.tabBarItem.title = "Top Rated"
    topRatedNavigationController.tabBarItem.image = UIImage(named: "top_rated")

    let searchStoryboard = UIStoryboard(name: "Main", bundle: nil)
    let searchNavigationController = searchStoryboard.instantiateViewControllerWithIdentifier("SearchNavController") as! UINavigationController
    let searchViewController = searchNavigationController.topViewController as! SearchViewController
    searchViewController.endpoint = "top_rated"
    searchNavigationController.tabBarItem.title = "Search"
    searchNavigationController.tabBarItem.image = UIImage(named: "Search")

    let tabBarController = UITabBarController()
    tabBarController.viewControllers = [nowPlayingNavigationController, topRatedNavigationController]

    window?.rootViewController = tabBarController
    window?.makeKeyAndVisible()
```

- Navigation Controller
```
    let storyboard = UIStoryboard(name:"Main", bundle: NSBundle.mainBundle())
    let newPostNav = storyboard.instantiateViewControllerWithIdentifier("NewPostNavigationController") as! UINavigationController
    let newPostVC = newPostNav.topViewController as! NewPostViewController
    newPostVC.newImg = editedImage
    presentViewController(newPostNav, animated: true, completion: nil)
```

- NSNotificationCenter
```
    NSNotificationCenter.defaultCenter().addObserverForName(User.userDidLogoutNotification, object: nil, queue: NSOperationQueue.mainQueue()) { (NSNotification) -> Void in
        let storyboard = UIStoryboard(name: "Main", bundle: nil)
        let vc = storyboard.instantiateViewControllerWithIdentifier("Lauch")
        self.window?.rootViewController = vc
    }
```

#### User Ineraction:

- Pull and Refresh
```
    refreshControl.addTarget(self, action: "refreshControlAction:", forControlEvents: UIControlEvents.ValueChanged)
            tableView.insertSubview(refreshControl, atIndex: 0)

    // MARK: - Refresh Control
    extension TweetsViewController {
        func refreshControlAction(refreshControl: UIRefreshControl) {
            offset = 20
            tweets = []
            loadMoreData()
            tableView.reloadData()
            refreshControl.endRefreshing()
        }
    }
//
```

- Infinite Scroll
```
    // MARK: - Infinite Scroll
    extension TweetsViewController: UIScrollViewDelegate {
        
        func scrollViewDidScroll(scrollView: UIScrollView) {
            if (!isMoreDataLoading) {
                // Calculate the position of one screen length before the bottom of the results
                let scrollViewContentHeight = tableView.contentSize.height
                let scrollOffsetThreshold = scrollViewContentHeight - tableView.bounds.size.height
                
                // When the user has scrolled past the threshold, start requesting
                if(scrollView.contentOffset.y > scrollOffsetThreshold && tableView.dragging) {
                    isMoreDataLoading = true
                    // Update position of loadingMoreView, and start loading indicator
                    let frame = CGRectMake(0, self.tableView.contentSize.height, self.tableView.bounds.size.width, InfiniteScrollActivityView.defaultHeight)
                    self.loadingMoreView?.frame = frame
                    self.loadingMoreView!.startAnimating()
                    TwitterClient.shareInstance.homeTimelineWithOffset(offset, success:{ (tweets: [Tweet]) -> () in
                        self.offset += 20
                        self.tweets = tweets
                        for (index,tweet) in tweets.enumerate() {
                            self.likeStates[index] = tweet.isFavorited
                            self.retweetStates[index] = tweet.isRetweeted
                        }
                        self.tableView.reloadData()
                        self.loadingMoreView?.stopAnimating()
                        self.isMoreDataLoading = false
                        }) { (error: NSError) -> () in
                            self.loadingMoreView?.stopAnimating()
                            print(error.localizedDescription)
                    }
                }
            }
        }
        func scrollViewSetup() {
            // Set up Infinite Scroll loading indicator
            let frame = CGRectMake(0, tableView.contentSize.height, tableView.bounds.size.width, InfiniteScrollActivityView.defaultHeight)
            loadingMoreView = InfiniteScrollActivityView(frame: frame)
            loadingMoreView!.hidden = true
            tableView.addSubview(loadingMoreView!)
            var insets = tableView.contentInset;
            insets.bottom += InfiniteScrollActivityView.defaultHeight;
            tableView.contentInset = insets
        }
    }
```


