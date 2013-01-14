The Global Federation of Assemblies
=====================================

Introduction
-------------

Reboot of Open Assembly based on 3 years on combat design and field testing and the latest technology that
make the original vision of Open Assembly more tangible and realistic. In reality the original vision
was not possible with Python/Django as an open source project, and the technology needed has only now matured.


Major features
---------------

* Federated - Clients can access multiple servers (once Meteor servers can connect to one another we can build a simple name server to share available servers)
* Movements - Dynamic Groups & Users
* Gamification - Classes, Rewards, and Currency System
* Easily Language Translation for Global Movement
* Locationally Aware using Mongo geospatial indexes (find sparks/users/etc near you)
* Extendable and Modular with various server level settings available

Dependencies
--------------

* Meteor
* Coffeescript (dev choice)
* jQuery
* jquery-cookie (meteor has no internal cookies yet)
* meteor-router (for handling multiple views, maybe backbone.js instead depending on Drew's comments)
* jQuery Lingua or equivalent
* GeoIP
* GeoLite Text Based Lat/Long Lookup

Models
--------

### User

User account ties the user to the system and stores any relevant extra information in an
attribute dictionary, allowing us to implement SMS, Picture verification, user location, or other features in the future easily.

> user = 

>>	mobile: "9188120430"

>>	location: "Tulsa, OK, USA"

>>	verified: true

>>	subscribed: ["asda9d79ad98ad98", "asd89a7sdasdy89a7d8yad7y"] # subscribed movements


### Movements

Dynamic Groups give players access to a way to easily store sparks in their relevant movement 
with very little overhead. Movement groups can be created dynamically similar to Twitter hashtags
but instead of being related to the content act as a container for sparks, actions, or subscribed users.

Movements can be lightwight. Links to the movement via _id are linked in Sparks, Actions, and user subscriptions.

> movement = 

>>	title: "OccupyWallStreet"

>>	spark_cnt: 37456

>>	user_cnt: 120457

>>	action_cnt: 67987

It is also possible to allow users within the group to define a group privacy setting via consensus, allowing for private or closed groups
that require an invite. The reason is this increases attractiveness for groups that are operating a clandestine operation or resistance
action that cannot be public. Rather than forcing these groups to roll their own server (which is ultimately a more secure option), making
the option to turn groups into private or closed by consensus of all members seems to be the best option which would allow new
movements to decide their own privacy.

#### Flat Hierarchy

There is no hierarchy. Either group functionality is open to all individuals or it is open to none. Therefore destructive
capability is relgated to administors, and only because it is impossible to stop them from manipulating the database anyways.

#### Why less control over groups?

Rather than making groups static objects, movements provides uers with ease of use and access. When creating a spark users can
create a new movement simultaneously, allowing new movements to easily arise from sparks. With no facilitator the group is ruled
by the voting produced by participators. 

### Sparks

Seed Idea, Problem/Solution, Issue, or Community Goal. Whatever the users want to make it. Users can plug currency into sparks, which is then
output to the actions that result from a spark. This incentivizes actions in the system and high quality sparks to attract funding
and subsequent actions to earn that funding. Once actions have been completed the Spark's rank decreases as it's funding base depletes.

Pushing currency into a Spark can only keep it afloat for a short period of time and the currency decays from the Spark with a small amount bleeding back into your account, however the taxes in that Spark do not return. This makes it important to invest in Sparks that are feasible

This allows users to keep Sparks rolling and keep actions going, even if 

* Content (Text, Videos, Images)
* Class (Environmentalist, Anarcho-Socialist, Conservative)

#### Spark functions and accessors:

* Pump X Reps into Spark -> Remove X Reps from User
* Comment on Spark

Sparks are rated by the amount of money they have but there is also the equivalent of rising and new rankings for sparks that take
into account other factors for viewing to allow new sparks to gain traction.


### Actions

* Content (Text, Videos, Images)

Actions earn more based on the amount of evidence/endorsements they receive. Actions can be endorsed or flagged as fakes, and if picture
evidence is present they earn more. If video is present it is also useful and will receive a bonus. As google glasses and other Augmented reality devices become more prominent it will be easier to share first person viewpoints of actions or pictures.

Anonymous actions can be taken that earn no repbucks. This is primarily to allow quasi-legal activities the user doesn't want tied to their account.


#### Action functions:

* Endorse(requires text statement of endorsement)
* Flag (flag as fake, requires text reason)

There is no real incentive to cheat the system, since there is no leaderboard, but reddit has shown that given an easily gamed system even
with no logical or tangible incentive people will cheat the system anyways. Therefore users should be able to flag functions
as fake, with reason, and then we will allow the general internet detectives to uncover the crimes of fraud. Tineye requires a huge fee
for API access but we can rely on users that might want to achieve Internet Detective related badges for uncovering confirmed fraud.

#### Limiter?

Add a limiter to actions so users cannot sit there and do fraudulent action after fraudulent action until a spark is dry. Fraudulent actions would be the only way to decrease the ranking of a spark, so we might want to limit the number of actions per day. In reality how many high quality activist actions could one partake in a single day? For instance protesting the police in Chicago was a day-long event, however it should really only count as a single spark. 

We might consider also using photo timestamp information to determine the time a photo was take and the likelihood it is a real photo. Of course this can be altered however that would increase the effort required to game the system.

### Pledge

A simple model, basically invoked when a user is planning or in the process of undergoing and action and wants to create a temporary
bookmark, or a pledge, to achieve some action based on a spark. The pledge can include the time of action, time of completion, to reward
users that consistently complete a pledge.

> pledge = 

>>	spark: "asdj7asd787sa8d78s"

>>	userId: "adakjsdiadioajdod"

>>	creationDate: "October 13, 1975 11:13:00"

>>	completionDate: "October 13, 1975 11:13:00"


### Comments

Comment system takes into account flaws of existing comment systems into its design. Some key ideas:

#### Top level comments are only shown. Child comments and lower must be expanded.

This reduces the users ability to attach their comments to parents to achieve a higher ranking.

#### 3 ways to Vote on a Comment

##### Reddit/Digg

* Upvote
* Downvote

##### Slashdot

* Interesting
* Off-Topic
* Funny

##### Google+/Facebook

* Like/Plus One


#### Downside to downvotes

Downvotes introduce a number of strategies to attack a comment. People will downvote what they do not agree with. Downvotes are supposed to be used for off-topic or bad content, rather than content you might disagree with that is high quality. Open Assembly originally introduced the idea of mult-dimension voting, but this concept was poorly understood.


#### Contextual Voting is Old but Good

Contextual voting offers us a way to integrate commenting into the game system without giving users EXP or Repbucks for comments. Since the voting is a mechanism
primarily to rank content, we can offer contextual voting similar to slashdot that is semantically related to the activist game system and use a simple point system to rank comments. Revolutionary, Informative, Funny, or some other semantic term can be flagged by the end user. The end user can specify what kind of content they like to see and the client will re-order the content in the browser.

This gives the ability to provide the user personalization without increasing the demand on the server.

**Semantic terms to be determined**

### Trust and Social Mechanisms

To establish a network for sharing actions internally. Add users to your trust network that you are comfortable with receiving new sparks from.

### Signals and Notifications

Since the gamification system is event based, as in you receive rewards as a result of an event, signals are required to ask the server
to run the necessary tests for each reward object related to the object type being created. Signal system can also delegate notification updates to the user.


### Federation

Main server stores a temporary listing of any other deployed servers until meteor.connect on the server allows us to extend this functionality to be a bit more automated. Alternatively one could use a simple HTTP nameserver, but it would be more powerful if the meteor servers themselves did lookup and discovery of other servers in the federation.

Users can subscribe to multiple servers, pick between servers, or integrate the published streams from all servers or a subset.


Gamification Models
--------------------

Gamification is a key feature of the reboot, giving more incentive to enter into the system even when there are not significant number of other users. Effectively the gamification is embedded in the system through the currency system, which gives users can incentive to take action. The gamification extends through rewards and classes. Rewards must be shaped to incentivize good use of the system, like completely pledges or cooperating with other users.

### Currency

Currency is generated through actions. A user can invest in sparks which increases the payoff from that spark
logarithmically. However even actions taken from an empty spark will produce some amount of currency. When another user takes an action on a spark they receive X amount of currency. As endorsements and evidence of the action is added they receive more currency. The maximum amount of currency in the system allowed is determined by the number of users. Payouts and taxes are determined so that the inflation of the system meets increase in the number of active users. Dead user accounts should not be included in this function.

#### Taxes and Death

Taxation in the system is required in some form to prevent inflation from spiralling out of control. Since there are no goods to purchase, inflation is not a life or death scenario however it will begin to increase the burden for new users to enter the system and feel as if their opinion is being counted. The initial taxation system will utilize a progressive tax to remove excess currency.

#### Transactions

Transactions in the system need to be tracked in order to facilitate refunds and analyze the flow of currency in the network.

### Rewards

Badges comprise the reward system with a user gaining badges for succesfully figuring out the interface, cooperating with other users, interacting with the currency system by pumping repbucks. Sharing links on other servers, committing actions, confirmed flagging of fraud. Badges could be rewarded for high quality comments or be related to class. The Rewards module is a series of reward models each including a test function that tests whether the user has qualified for the reward.

> reward = 

>>	template: 'template_key'

>>	user: userId

> reward_test =

>>	template: 'template_key'

>>	test: (user) -> test user

Badges are expressed through a database test and a template key. Badge templates are stored in a dictionary on the server, and can be accessed when needed. THis

> templateDict =

>>	action_creation_5: Meteor.Template.action_creation_5

>>	action_creation_10: Meteor.Template.action_creation_10

>>	action_creation_25: Meteor.Template.action_creation_25


This would be useful for grabbing badges with a single DB call and iterating through the list directly rendering each by template.


### Class

Classes offer a way for users to tag sparks based on the type of activism, whether it's internet hacking, environmental, conservative, or whatever. Spark authors are encouraged to add a class to their spark, and users can create new classes if they don't like the existing ones. Similar to tags, except you gain experience points in different classes which allow your character to level that class. This effectively allows the users to shape the type of Augmented Reality RPG they are playing, and shape the image they portray within the game.

#### Functions

* Browse Classes and Add to a Spark
* Add a new Class

### Experience Points

Users gain experience points in each individual class. These points can probably be stored in the User module. There are no rankings based on experience points, and no caps on levels although it becomes exponentially more difficult to gain levels over time. While the currency system looks to equalize the ability of the users to effect the system, amongst active users undergoing actions, the experience points are meant to purely reward users who act the most in certain domains they are most interested in.

There are no limit to the number of classes a user can undergo. Users can also gain experience points for good sparks, and receive modifiers based on comment voting. I.e. a user could become a Level 11 revolutionary anarcho-socialist if they undertook anarcho-socialist actions and made revolutionary comments.


Server-Side Only
------------------

### Parser

Parses a string of text and parses any links which are then parsed for content. Server side because we might do some basic page crawling to grab metadata from outside links.


Views
--------

There are effectively 3 types of views. There are list views, content views, and site views. List views show lists of data
the user is interested in, content views show sparks, actions, or users, and site views are for other simple things like
about pages.

### Lists

#### Users

See groups of users based on movements, in your locational vicinity, 

#### Sparks/Actions

Sparks and Actions based on user Movement subscriptions, locational vicinity, etc.

#### Servers

Primarilty for Federation purposes

### Content Views

#### User

User public information, gamification states, user contributions

#### Spark

Spark info and content, comment list

#### Acton

Action info and content, comment list

### Site views

* About Page
* FAQ with more details