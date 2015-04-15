### Brief Explaination

เดิมทีแล้วเวลาเรา login เข้ามา ระบบจะเก็บ `User` ไว้ใน `session()` โดยที่เก็บในลักษณะ Hashmap คือ<br>
เราสั่ง `session("username", <username>)`<br>
เก็บ `<username>` ที่รับมา (เป็น string) และใช้ `key` ชื่อว่า "username" ไว้สำหรับเรียกใช้หลังจากนี้

ซึ่งการที่หน้า page แต่ละหน้าจะรู้ได้ว่าใครกำลัง login อยู่เราก็สามารถเช็คได้จาก `session()`<br>
โดยการเรียก `session().get("username")` แล้วเราจะได้ <username> ที่เป็น string มาเอาไป find หา User ได้

ดังนั้นการที่จะเช็คว่าถ้าไม่มีใครล็อคอินอยู่ให้เด้งกลับไปที่หน้าแรกจึงทำได้โดย

# โค้ดอันนี้ไม่ต้องเขียนโว้ย แค่อธิบายว่ามันทำงานยังไง ไปทำตาม STEP ข้างล่าง

	User user = User.find.where().eq("username", session().get("username")).findUnique();
	if (user != null) {
		//ถ้ามี user login ให้ไปลิ้งนี้
        return ok(test.render(user));
    } else {
    	//ถ้าไม่มีให้ไปลิ้งนี้
        return ok(error.render("No user"));
    }
    
เพราะงั้นเราจะต้องเขียนโค้ดแบบนี้ให้กับทุก ๆ page ที่ต้องการ user ที่ login แล้วเท่านั้นถึงมี permission ในการเข้าถึง
แล้วในเมื่อมันลำบาก play framework ก็เลยมีอะไรช่วยให้มันไม่ลำบากโดยการที่มีตัว **Authenticator มาให้เราเช็คโดยเฉพาะ**

## Step
### ใช้ Authenticator

1. Rename `SecurityController.java` to `Secured.java` (เหตุผลคือชื่อแม่งยาวไป เอาตามที่ guide สอนมาดีกว่า)

2. `class Secured extends Security.Authenticator` (`import play.mvc.Security`)

3. click code > override methods > select `onUnauthorized` and `getUsername` > click ok

4. modify return statement of `getUsername` to `return context.session().get("username");`

5. modify return statement of `onUnauthorized` to `return redirect(routes.Application.login());`

6. Add `@Security.Authenticated(Secured.class)` above method to
	- `Application.team()`
	- `Application.user()`
	- `ProjectController.project()`
	- `ProjectController.projectlist()`
	- `VoteController.vote()`
	- `VoteController.result()`
	- `ProjectController.addProjectPage()`

7. Run and test if bug
