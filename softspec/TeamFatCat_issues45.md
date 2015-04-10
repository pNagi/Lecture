### USER

1. Change `Finder<Long, User> find` access modifiers to `private`

2. Add methods

  - getAllUsers()
    1. Application.user()
    2. Application.addUser()
    3. Application.team()
  
  - deleteUserById(long id)
    1. Application.clearUsers()
  
  - findById(long id)
    1. ProjectController.project()
    2. ProjectController.projectlist()
    3. VoteController.manageVote()
    4. VoteController.vote()
    5. Team.getMembers()
  
  - findByUsername(String username)
    1. Application.test()
    2. Application.authenticate()
    3. Application.addMember()
