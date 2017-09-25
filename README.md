# Udacity-Interview-Question


### 1.What have you learned recently about iOS development? How did you learn it? Has it changed your approach to building apps?

I have recently completed and mastered the uses of more advanced features of the Swift programming language.
 
I now know that having a thorough understanding of advanced language features of Swift is so powerful. As a swift developer, you can alter the programming language as you want, according to your needs using various design patterns including class extensions, delegation, protocols, typealises and so on. This allows you to focus on building your own reusable code that can be used for all of your work.

I use a great dependency manager called Cocoapods that allows me to package up my components into reusable modules. This way, I can apply into any of my project. Mastering the intricacies of the Swift programming language has taught me to be efficient and also changed how I build software.
 
Next thing that I learned this past year is how to apply the best practices and adjust to my work. I believe I became a better developer after this and I can apply my knowledge to solve more complicated problems in a team. For example, I now know how to record my work, use Git for my iOS and web development. I can use Git so much better by writing very detailed commit messages by using early, rebasing and squashing my commits. These not only help me to create better software, but I can also help people in my team greatly.
 
### 2.Can you talk about a framework that you've used recently (Apple or third-party)? What did you like/dislike about the framework?

I also learned to use CoreData and Realm data persistence frameworks by reading and studying the documentations and actually practicing using API in similar applications.
 
I like CoreData because of its high power and potential. It is especially useful and powerful when using its API for large scale desktop and mobile applications. However, one down side is its high cost. It is hard to fully attain the knowledge and to gain full understanding of CoreData Stack to build a perfect software. I now know the power of CoreData, but I believe that is not the best solution for every mobile applications.
 
I especially like to use the Realm persistence framework because it is specified for the mobile platform. With this, you can always run your persistence logic on many different threads without bad access or data corruption. I will use this framework when it is suitable, and at the same time, I am curious to find out how to use Realm for smaller applications.
 

### 3.Describe how you would construct a Twitter feed application (here is an example of Udacity's Twitter feed) that at minimum can display a company's Twitter page. Please include information about any classes/structs that you would use in the app. Which classes/structs would be the model(s), the controller(s), and the view(s)?

I believe that the first step to writing good software is to break down the requirements and specifications in a highly detailed manner. Once the specifications are mapped out, I would structure the application's data structs and classes following the Model View Controller paradigm. An example architecture is shown below.

Model

The Model classes are responsible for downloading data from the Twitter API, storing tweets, account and organization data, and persisting the data using CoreData. There is a CoreDataStackManager class for all CoreData operations and also an ImageCache class for caching any images downloaded.

--------------------------
|Class	Inherits From|
|Tweet	NSManagedObject|
|Account	NSMangedObject|
|TwitterAPI	NSObject|
|Organization	NSManageObject|
|ImageCache	NSObject|
|CoreDataStackManager	N/A|
---------------------------

View

For custom views, there is a custom tableview cell for showing the detail of each tweet in the feed. To customize the UI, there is a Like button for liking a tweet, a Twitter login button and custom views for the settings and login views. There are also other various custom UI elements, such as the action buttons within each tweet cell in the feed.

Class	Inherits From
LikeButton	UIButton
TweetTableViewCell	UITableViewCell
LoginButton	UIButton
SettingsView	UIView
LoginView	UIView
Controller

The controller classes are responsible for controlling the UI for the various components of the app. There is a tab view for navigating between scenes from the main view, a navigation controller for drilling down to the detail of a tweet, a detail view for showing a single tweet, and a view controller for the account and organization views.

Class	Inherits From
AccountViewController	UIViewController
TweetViewController	UIViewController
AccountViewController	UIViewController
TweetViewController	UIViewController
FeedViewController	UITableViewController
OrganizationViewController	UIViewController
NavigationController	UINavigationController
TabBarViewController	UITabBarController
LoginViewController	UIViewController
ComposeTweetViewController	UIViewController
SettingsViewController	UIViewController
Other

There are also other custom classes, such as the TransitionDelegate, PhotoAnimator, and others, which will help to build a cohesive custom UI with beautiful transition animations.

Class	Inherits From
TransitionDelegate	UIViewControllerTransitioningDelegate
PhotoPresentationAnimator	UIViewControllerAnimatedTransitioning
Although the above list is not completely exhaustive, it outlines a great start to building a fantastic Twitter app.

### 4.Describe some techniques that can be used to ensure that a UITableView containing many UITableViewCell is displayed at 60 frames per second.

This curiosity is the one when the developers often forget to take into the account when building a good software, which is a performance. I can confidently say that I am performance-oriented developer. So I will plan out how I would design and test my UITableView to display at least 60 FPS.
 
First, for instance, Engineers in Apple put a lot of time and effort in to create a user interface library with great deal of performance. This method of dequeing reusable cells is good. The basis here is that instead of performing complicated operations to make a new cell every time, we can simply recycle these cells. Then when they are no longer in the sight, we can update the state of view elements with new data and use it.
 
Here, it is when Apple’s delegate pattern comes in. We utilize the ‘UITableViewDelegate/Datasource’ methods in a very intelligent manner. So that they can hold the power and optimize the process that Apple employees have perfected it with so much time and effort. The example would be that instead of binding the data to the entire tableview and all the cells, we can use ‘tableView:sillDisplayCEll:forRowAtIndexPath’ method to calculate only the changes in each cell when the cell is about to come out.
 
Because the performance of the talbeview depends on these delegate and datasource methods, we have to pay close attention when use these methods. Recycling pattern is effective, but it can take complex calculations from within the delegate and datasource methods. These complicated data operations have to happen on the background dispatch queues. Another thing is that it is good to keep the tableview very simple as far as the dimensions. This is because the calculations for ‘heightForRowAtIndexPath’ and other methods are completed on each pass when the new cells in tableview are created.

When I consider the view drawing lifecycle for any custom views rendered within the tableview cell, I want to use the least expensive graphics operations. This means that I would like to avoid heavy animations for Apple’s CoreAnimation framework. So instead of that, I can do our view rendering using CoreGraphis ‘drawRect’ way. What this does is that it is good for rendering custom static content through the CPU. From what I understand, this frees up the GPU to take more complex graphics that UIKit performs.
 
For testing my theories, I can use the Apple Instruments applications to measure at which speed at which our tableview cells were being rendered. Then I can tweak it until I get it above 60 FPS.


### 5. Imagine that you have been given a project that has this ActorViewController. The ActorViewController should be used to display information about an actor. However, to send information to other ViewControllers, it uses NSUserDefaults. Does this make sense to you? How would you send information from one ViewController to another one?

Using ```NSUserDefaults``` does not right solution for persisting any data other than user settings. The alternative way that I suggest would be using CoreData. I would recommend creating a separate NSManagedObject model class for the Actor. The class could be accessed through the fetchedResultsController from within any ViewController and we could save data using one or more managedObjectContexts created in a CoreDataStackManager class.

Below is a bit of pseudo-code showing how the model class would be structured.

### 6. Imagine that you have been given a project that has this GithubProjectViewController. The GithubProjectViewController should be used to display high-level information about a GitHub project. However, it’s also responsible for finding out if there’s network connectivity, connecting to GitHub, parsing the responses and persisting information to disk. It is also one of the biggest classes in the project. Follow-up question:: How might you improve the design of this view controller?

If one of my team members gave me a file for ViewController that has a code for fetching and storing data from a network to the local device, I will suggest to take the Udacity iOS Developer Nanodegree . Then I would help them so that they could improve their code.
 
To begin, I would reevaluate the code into separate classes. First, I create a model class for storing the data to a persistent store, and create a separate ‘GithubAPI’ model class. This is because it handled the network requests and data parsing. After this, the code will be better and it will abide by the Model View Controller paradigm. This makes the code more reusable, recycled, decoupled and easier to detect debug.
 
I have come up with a pseudo-code that I saved in the `GitHubProjectViewController.swift` file to demonstrate this.

### 7.If you were to start your iOS developer position today, what would be your goals a year from now? 

For my future, after a year, I will have completed another two Nanodegress that will allow me to become a better and more effective software developer. I will have gained deeper understanding of the entire development process. I also would like to be leading a team and be a mentor for other aspiring software developer. From now on, I will utilize all of my new set of skills and practices to create outstanding and extraordinary products for the company that I work for.
 
I can be sure that the jobs that I apply will help me to grow and reach my professional goals. With the company’s help, I will be able to grow and multiply my passion along with their goals and missions. After working at Udacity, I will be learning from my colleagues and be applying my obtained skills to help others to learn. I am so happy to help others to learn and share our knowledge and skills with each other to grow together. Udacity helped me and gave me so many opportunities to be a leader so far. I am thrilled to have more opportunities to create tools that would help Udacity.
 
I will not stop here and continue on my professional and personal growth path using my skills that I learned, and incorporating them into my passion, which is to help other people to learn and to work together beneficially.

