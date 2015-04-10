### User.java

1. Change `Finder<Long, User> find` access modifiers to `private`

2. Add methods to `User.java`

 ###### getAllUsers()
 ```
 public static List<User> getAllUsers() {
    return find.all();
 }
 ```
  then modify following method(s) from `User.find.all()` to `User.getAllUsers()`
  
   1. Application.user()
   2. Application.addUser()
   3. Application.team()
  
 ##### deleteUserById(long id)
 ```
 public static void deleteById(long id) {
    find.ref(id).delete();
 }
 ```
  then modify following method(s) from `User.find.red(<id>).delete()` to `User.deleteById(<id>)`
  
   1. Application.clearUsers()
  
 ##### findById(long id)
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

 ##### findByUsername(String username)
 ```
 public static User findByUsername(String username) {
    return find.where().eq("username", username).findUnique();
 }
 ```
    
  then modify following method(s) from `User.find.where().eq("username", <username>).findUnique()` to `User.findByUsername(<username>)`
  
   1. Application.test()
   2. Application.authenticate()
   3. Application.addMember()

### Team.java

1. Change `Finder<Long, User> find` access modifiers to `private`

2. Add methods to `Team.java`

 ##### getAllTeams()
 ```
 public static List<Team> getAllTeams() {
    return find.all();
 }
 ```
  then modify following method(s) from `Team.find.all()` to `Team.getAllTeams()`
  
   1. Application.team()
   2. ProjectController.addProjectPage
 
 ##### findById()
 ```
 public static Team findById(long id) {
    return find.byId(id);
 }
 ```
 
  then modify following method(s) from `Team.find.byId(<id>)` to `Team.findById(<id>)`
  
   1. Application.removeMemberFromTeam()
   2. ProjectController.project()
 
 ##### findByName()
  ```
 public static Team findByName(String name) {
    return find.where().eq("name", name).findUnique();
 }
 ```
    
  then modify following method(s) from `Team.find.where().eq("name", <name>).findUnique()` to `Team.findByName(<name>)`
  
   1. Application.addMember()


#### Repeat this for Vote.java and Project.java

__Steps__

 1. change accessibility of `find` to private
 2. run in localhost
 3. see which part need to fixed
 4. create a new method in models
 5. then in controller make it call new method that you just create (instead of using for find)
 6. Repeat 2-6 until it can run

อาจจะมาเขียนต่อให้ละเอียดกว่านี้ถ้าไม่ขี้เกียจ
