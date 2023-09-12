# <a href="https://leetcode.com/problems/design-twitter/description/" target="_blank">355 Design Twitter</a>

## Problem

Design a simplified version of Twitter where users can post tweets, follow/unfollow another user, and is able to see the 10 most recent tweets in the user's news feed.

Implement the Twitter class:

Twitter() Initializes your twitter object.
void postTweet(int userId, int tweetId) Composes a new tweet with ID tweetId by the user userId. Each call to this function will be made with a unique tweetId.
List<Integer> getNewsFeed(int userId) Retrieves the 10 most recent tweet IDs in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user themself. Tweets must be ordered from most recent to least recent.
void follow(int followerId, int followeeId) The user with ID followerId started following the user with ID followeeId.
void unfollow(int followerId, int followeeId) The user with ID followerId started unfollowing the user with ID followeeId.
 

Example 1:

Input
["Twitter", "postTweet", "getNewsFeed", "follow", "postTweet", "getNewsFeed", "unfollow", "getNewsFeed"]
[[], [1, 5], [1], [1, 2], [2, 6], [1], [1, 2], [1]]
Output
[null, null, [5], null, null, [6, 5], null, [5]]

Explanation
Twitter twitter = new Twitter();
twitter.postTweet(1, 5); // User 1 posts a new tweet (id = 5).
twitter.getNewsFeed(1);  // User 1's news feed should return a list with 1 tweet id -> [5]. return [5]
twitter.follow(1, 2);    // User 1 follows user 2.
twitter.postTweet(2, 6); // User 2 posts a new tweet (id = 6).
twitter.getNewsFeed(1);  // User 1's news feed should return a list with 2 tweet ids -> [6, 5]. Tweet id 6 should precede tweet id 5 because it is posted after tweet id 5.
twitter.unfollow(1, 2);  // User 1 unfollows user 2.
twitter.getNewsFeed(1);  // User 1's news feed should return a list with 1 tweet id -> [5], since user 1 is no longer following user 2.
 

Constraints:

1 <= userId, followerId, followeeId <= 500
0 <= tweetId <= 104
All the tweets have unique IDs.
At most 3 * 104 calls will be made to postTweet, getNewsFeed, follow, and unfollow.

---

## Solution

```python
from collections import defaultdict

class Twitter:

    def __init__(self):
        # Initialize a dictionary to keep track of which users each user follows.
        # Default value for each user (key) is an empty set.
        self.userId2Followees = defaultdict(set)

        # Initialize a list to store all tweets as pairs (userId, tweetId).
        self.posts = []

    def postTweet(self, userId: int, tweetId: int) -> None:
        # Append a new tweet as a tuple (userId, tweetId) to the posts list.
        self.posts.append((userId, tweetId))

    def getNewsFeed(self, userId: int):
        # Initialize a counter to keep track of the number of tweets added to the news feed.
        count = 0

        # Initialize an empty list to store the tweets that will be returned as the user's news feed.
        feed = []

        # Loop backwards through the posts list (from most recent to least recent).
        # 
        #      [(1, 5), (2, 6),   ...,     (7323, 4323)]
        #  -1     0        1            len(self.posts) - 1
        #  ( ) <-------<--------<------<----------^
        for i in range(len(self.posts) - 1, -1, -1):
            # Break out of the loop if 10 tweets have already been added to the news feed.
            if count >= 10:
                break
            
            # Fetch the current tweet.
            post = self.posts[i]
            
            if (
                post[0] == userId                               # If the tweet was posted by the user
                or post[0] in self.userId2Followees[userId]     # or by someone the user follows
            ):
                # then add it to the news feed.
                feed.append(post[1])
                count += 1

        # Return the news feed.
        return feed

    def follow(self, followerId: int, followeeId: int) -> None:
        # Add the followeeId to the set of users that the followerId user is following.
        self.userId2Followees[followerId].add(followeeId)

    def unfollow(self, followerId: int, followeeId: int) -> None:
        # If the followerId user is following the followeeId user, remove the followeeId from the set.
        if followeeId in self.userId2Followees[followerId]:
            self.userId2Followees[followerId].remove(followeeId)

```

Let's analyze the time and space complexity for each method:

1. **`__init__`**:
   - Time Complexity: \(O(1)\)
   - Space Complexity: \(O(1)\) 
   (Although we're initializing a dictionary and a list, they start empty, so the initialization is constant time and space.)

2. **`postTweet`**:
   - Time Complexity: \(O(1)\) 
   (Appending to a list is a constant-time operation on average.)
   - Space Complexity: \(O(1)\) 
   (We're only adding one item to the list.)

3. **`getNewsFeed`**:
   - Time Complexity: \(O(N)\) 
   (Where \(N\) is the number of posts. In the worst case, we'd iterate through all the posts, but this is bounded by the condition that at most 10 tweets are added to the feed.)
   - Space Complexity: \(O(1)\) 
   (We're only using a fixed amount of extra space for variables `count`, `feed`, and `post`. The space required for the `feed` list is bounded by 10.)

4. **`follow`**:
   - Time Complexity: \(O(1)\) 
   (Adding to a set is a constant-time operation on average.)
   - Space Complexity: \(O(1)\)

5. **`unfollow`**:
   - Time Complexity: \(O(1)\) 
   (Checking membership in a set and removing an element from it are both constant-time operations on average.)
   - Space Complexity: \(O(1)\)

Considering the overall data structures:

- `userId2Followees`: The space complexity grows with the number of users and the number of followee relationships. In the worst case (each user follows every other user), it becomes \(O(U^2)\) where \(U\) is the number of users.
- `posts`: The space complexity grows with the number of tweets, \(O(T)\) where \(T\) is the number of tweets.

So, the overall space complexity considering all data structures and methods can be thought of as \(O(U^2 + T)\), but for the specific methods listed above, the space complexities mentioned apply.
