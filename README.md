# getKeyBoardHeight-with-Notifications

- (void)viewDidLoad {
    [super viewDidLoad];

    [self KeyboardNotifications];
    
}

-(void)viewDidAppear:(BOOL)animated {
    [super viewDidAppear:YES];
    self.contentInsetTop = self.collectionView.contentInset.top;
    self.contentInsetBottom = self.collectionView.contentInset.bottom;
}

- (void)KeyboardNotifications
{
    [[NSNotificationCenter defaultCenter] addObserver:self
                                             selector:@selector(keyboardWasShown:)
                                                 name:UIKeyboardDidShowNotification object:nil];
    
    [[NSNotificationCenter defaultCenter] addObserver:self
                                             selector:@selector(keyboardWillBeHidden:)
                                                 name:UIKeyboardWillHideNotification object:nil];
    
}

- (void)keyboardWasShown:(NSNotification*)aNotification
{
    NSDictionary* info = [aNotification userInfo];
    CGSize keyboardSize = [[info objectForKey:UIKeyboardFrameBeginUserInfoKey] CGRectValue].size;
    
  //Adjust inset with keyboard Size to scroll to specified indexPath below

    UIEdgeInsets contentInsets = UIEdgeInsetsMake(self.contentInsetTop, 0.0, keyboardSize.height, 0.0);
    
    self.collectionView.contentInset = contentInsets;
    self.collectionView.scrollIndicatorInsets = contentInsets;
    
    NSIndexPath *indexPath = [self.collectionView indexPathsForSelectedItems][0];
    [self.collectionView scrollToItemAtIndexPath:indexPath atScrollPosition:UICollectionViewScrollPositionCenteredVertically animated:YES];

}

- (void)keyboardWillBeHidden:(NSNotification*)aNotification
{ 
  //Dismissing the keyboard and restoring to orignal contentInsets
    UIEdgeInsets contentInsets = UIEdgeInsetsMake(self.contentInsetTop, 0.0, self.contentInsetBottom, 0.0);
    self.collectionView.contentInset = contentInsets;
    self.collectionView.scrollIndicatorInsets = contentInsets;
    
}
