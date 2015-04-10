### USER

1. Change `Finder<Long, User> find` access modifiers to `private`

2. Add methods

 - getAllUsers()
 ```
 public static List<User> getAllUsers() {
    return find.all();
 }
 ```
  then modify following method(s) from `User.find.all()` to `User.getAllUsers()`
  
   1. Application.user()
   2. Application.addUser()
   3. Application.team()
  
 - deleteUserById(long id)
 ```
 public static void deleteById(long id) {
    find.ref(id).delete();
 }
 ```
  then modify following method(s) from `User.find.red(<id>).delete()` to `User.deleteById(<id>)`
  
   1. Application.clearUsers()
  
 - findById(long id)
 ```
 public static User findById(long id) {
    return find.byId(id);
 }
 ```
  then modify following method(s) from `User.find.byId(<id>)` to `User.findById(<id>)`
  
   1. ProjectController.project()
   2. ProjectController.projectlist()
   3. VoteController.manageVote()
   4. VoteController.vote()
   5. Team.getMembers()

 - findByUsername(String username)
 ```
 public static User findByUsername(String username) {
    return find.where().eq("username", username).findUnique();
 }
 ```
    
  then modify following method(s) from `Userfind.where().eq("username", <username>).findUnique()` to `User.findByUsername(<username>)`
  
   1. Application.test()
   2. Application.authenticate()
   3. Application.addMember()
