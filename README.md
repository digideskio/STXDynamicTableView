#STXDynamicTableView

`STXDynamicTableView` is designed to solve the common use case to display a feed of photos with their corresponding likes, caption, and comments. It's inspired by Instagram feed table view.

<div align="center">
<tr>
    <td>
        <img src="http://engineering.2359media.net/media/2014-04-16-rebuilding-instagram-feed-table-view/images/feed1.png" width="266" height="500" />
    </td>
    <td>
        <img src="http://engineering.2359media.net/media/2014-04-16-rebuilding-instagram-feed-table-view/images/feed2.png" width="266" height="500" />
    </td>
    <td>
        <img src="http://engineering.2359media.net/media/2014-04-16-rebuilding-instagram-feed-table-view/images/feed3.png" width="266" height="500" />
    </td>
</tr>
</div>

---
##Usage

Import the whole `STXDynamicTableView` source files into your project, and import the main header file:

     #import "STXDynamicTableView.h"

Supply your table view in the view controller, then set the delegate and data source:

    STXFeedTableViewDataSource *dataSource = [[STXFeedTableViewDataSource alloc] initWithController:self tableView:self.tableView];
    self.tableView.dataSource = dataSource;
    self.tableViewDataSource = dataSource;
    
    STXFeedTableViewDelegate *delegate = [[STXFeedTableViewDelegate alloc] initWithController:self];
    self.tableView.delegate = delegate;
    self.tableViewDelegate = delegate;

Populate your data models to the table view data source:

    NSDictionary *instagramPopularMediaDictionary = [jsonObject objectWithJSONSafeObjects];
    if (instagramPopularMediaDictionary) {
        id data = [instagramPopularMediaDictionary valueForComplexKeyPath:@"data"];
        NSArray *mediaDataArray = [data objectWithJSONSafeObjects];
        
        NSMutableArray *posts = [NSMutableArray array];
        for (NSDictionary *mediaDictionary in mediaDataArray) {
            STXPost *post = [[STXPost alloc] initWithDictionary:mediaDictionary];
            [posts addObject:post];
        }
        
        self.tableViewDataSource.posts = [posts copy];
        
        [self.tableView reloadData];
    }

Your data models need to conform to `STXPostItem`, `STXCommentItem`, and `STXUserItem` to be able to use the built-in table view data source and delegate.

---
##Background

Read [Rebuilding Instagram feed table
view](http://engineering.2359media.net/blog/2014/04/16/rebuilding-instagram-feed-table-view/) to understand the challenges, difficulties, and how do we solve the issue of rebuilding the table view style popularized by Instagram app with Auto Layout.

---
##Disclaimer
`STXDynamicTableView` is simply a reusable code that you can use in your own project for any purpose as outlined in the LICENSE file. It's not a fully-fledged library, although we're taking steps to go there as time allows.

___
##Feedback
We'd love to hear feedback. Create Github issues, pull requests, or hit us up on [Twitter](http://twitter.com/2359eng).

___
##License
`STXDynamicTableView` is available under the MIT license. See the LICENSE file for more info.



