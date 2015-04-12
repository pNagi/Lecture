1. Rename `SecurityController.java` to `Secured.java` (เหตุผลคือชื่อแม่งยาวไป เอาตามที่ guide สอนมาดีกว่า)

2. `class Secured extends Security.Authenticator` (`import play.mvc.Security`)

3. click code > override methods > select `onUnauthorized` and `getUsername` > click ok

4. modify return statement of `getUsername` to `return context.session().get("username");`

5. modify return statement of `getUsername` to `return redirect(routes.Application.login());`

6. Add `@Security.Authenticated(Secured.class)` above method to
	- `Application.team()`
	- `Application.user()`
	- `ProjectController.project()`
	- `ProjectController.projectlist()`
	- `VoteController.vote()`
	- `VoteController.result()`
	- `ProjectController.addProjectPage()`

7. แปปลืมเขียนข้อ 7
8. Run and test if bug
