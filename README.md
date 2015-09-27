# Access the keyboard height dynamically

Keyboard Notifications 

Code example shows how to get the keyboard Height while using a collectionView

- (void)viewDidLoad {
    [super viewDidLoad];

    [self setUpKeyboardNotifications];
    
}

-(void)viewDidAppear:(BOOL)animated {
    [super viewDidAppear:YES];
    //Getting original contentInsets of collectionView  
    //tableView.contentInsets should be zero
    
    self.contentInsetTop = self.collectionView.contentInset.top;
    self.contentInsetBottom = self.collectionView.contentInset.bottom;
}

- (void)setUpKeyboardNotifications
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
    
      // Now adjust inset with keyboard Size to scroll to specified indexPath below


}

- (void)keyboardWillBeHidden:(NSNotification*)aNotification
{ 
  // Dismissing the keyboard and restoring to orignal contentInsets and indexPaths

}
    
