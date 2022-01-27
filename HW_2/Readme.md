                                                HW_2 Postman
```

				http://162.55.220.72:5005/first

1. Отправить запрос.
	save -> send -> This is the first responce from server!

2. Статус код 200
	
	pm.test("Status code 200", function () { 
   	 pm.response.to.have.status(200); 
	});

3. Проверить, что в body приходит правильный string.
	
	pm.test("В body правильный string", function () { 
    	pm.response.to.have.body("This is the first responce from server!");
	});

			
				http://162.55.220.72:5005/user_info_3

	name: Klim ;	age: 39;	salary: 500;
1. Отправить запрос.
	save -> send

2. Статус код 200
	
	pm.test("Status code 200", function () {
    	pm.response.to.have.status(200);
	});

3. Спарсить response body в json.
	
	let resBody = pm.response.json();

4. Проверить, что name в ответе равно name s request (name вбить руками.)
	
	pm.test("name", function () {
    	pm.expect(resBody.name).to.eql("Klim");
	});

5. Проверить, что age в ответе равно age s request (age вбить руками.)
	
	pm.test("age", function () {
	pm.expect(resBody.age).to.eql("39");
	});

6. Проверить, что salary в ответе равно salary s request (salary вбить руками.)
	
	pm.test("salary",function () {
    	pm.expect(resBody.salary).to.eql(500);
	});

7. Спарсить request.
	
	let req = request.data;

8. Проверить, что name в ответе равно name s request (name забрать из request.)
	
	pm.test("name c Body", function () {
    	pm.expect(resBody.name).to.eql(req.name);
	});

9. Проверить, что age в ответе равно age s request (age забрать из request.)
	
	pm.test("age c Body", function () {
    	pm.expect(resBody.age).to.eql(req.age);
	});

10. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
	
	pm.test("salary c Body", function () {
   	pm.expect(resBody.salary).to.eql(+req.salary);
	});

11. Вывести в консоль параметр family из response.
	
	console.log(resBody.family);

12. Проверить что u_salary_1_5_year в ответе равно salary*4 (salary забрать из request)
	
	pm.test("u_salary_1_5_year", function () {
    	pm.expect(resBody.family.u_salary_1_5_year).to.eql(req.salary*4);
	});


				http://162.55.220.72:5005/object_info_3

	http://162.55.220.72:5005/object_info_3?name=Klim&age=39&salary=500

1. Отправить запрос.
	save -> send

2. Статус код 200
	
	pm.test("Status code 200", function () {
   	pm.response.to.have.status(200);
	});

3. Спарсить response body в json.
	
	let resBody = pm.response.json();

4. Спарсить request.
	
	let req = pm.request.url.query.toObject();

5. Проверить, что name в ответе равно name s request (name забрать из request.)
	
	pm.test("name_is", function () {
    	pm.expect(resBody.name).to.eql(req.name);
	});

6. Проверить, что age в ответе равно age s request (age забрать из request.)
	
	pm.test("age_is", function () {
    	pm.expect(resBody.age).to.eql(req.age);
	});

7. Проверить, что salary в ответе равно salary s request (salary забрать из request.)
	
	pm.test("salary_is", function () {
    	pm.expect(resBody.salary).to.eql(+req.salary);
	});

8. Вывести в консоль параметр family из response.
	
	console.log(resBody.family);

9. Проверить, что у параметра dog есть параметры name.
	
	pm.test("У_dog_есть_name", () => {
    	pm.expect(resBody.family.pets.dog).to.have.property("name");
	});

10. Проверить, что у параметра dog есть параметры age.
	
	pm.test("У_dog_есть_age", () => {
   	 pm.expect(resBody.family.pets.dog).to.have.property("age");
	});

11. Проверить, что параметр name имеет значение Luky.
	
	pm.test("У_dog_есть_имя_Luky", () => {
    	pm.expect(resBody.family.pets.dog.name).to.be.oneOf(["Luky"]);
	});

12. Проверить, что параметр age имеет значение 4.
	
	pm.test("У dog age 4", () => {
    	pm.expect(resBody.family.pets.dog.age).to.be.oneOf([4]);
	});


				http://162.55.220.72:5005/object_info_4

	http://162.55.220.72:5005/object_info_4?name=Klim&age=39&salary=500
1. Отправить запрос.
	save -> send

2. Статус код 200
	
	pm.test("Status code 200", function () {
    	pm.response.to.have.status(200);
	});

3. Спарсить response body в json.
	
	let resBody = pm.response.json();

4. Спарсить request.
	
	let req = pm.request.url.query.toObject();

5. Проверить, что name в ответе равно name s request (name забрать из request.)
	
	pm.test("name_is", function () {
    	pm.expect(resBody.name).to.eql(req.name);
	});

6. Проверить, что age в ответе равно age из request (age забрать из request.)
	
	pm.test("age_is", function () {
    	pm.expect(resBody.age).to.eql(+req.age);
	});

7. Вывести в консоль параметр salary из request.
	
	console.log("salary из request", req.salary);

8. Вывести в консоль параметр salary из response.
	
	console.log("salary из response", resBody.salary);

9. Вывести в консоль 0-й элемент параметра salary из response.
	
	console.log("salary 0-й элемент", resBody.salary[0]);

10. Вывести в консоль 1-й элемент параметра salary параметр salary из response.
	
	console.log("salary 1-й элемент", resBody.salary[1]);

11. Вывести в консоль 2-й элемент параметра salary параметр salary из response.
	
	console.log("salary 2-й элемент", resBody.salary[2]);

12. Проверить, что 0-й элемент параметра salary равен salary из request (salary забрать из request.)
	
	pm.test("Salary[0]", function () {
    	pm.expect(resBody.salary[0]).to.eql(+req.salary);});

13. Проверить, что 1-й элемент параметра salary равен salary*2 из request (salary забрать из request.)
	
	pm.test("Salary[1]", function () {
    	pm.expect(+resBody.salary[1]).to.eql(req.salary*2);});

14. Проверить, что 2-й элемент параметра salary равен salary*3 из request (salary забрать из request.)
	
	pm.test("Salary[2]", function () {
    	pm.expect(+resBody.salary[2]).to.eql(req.salary*3);});

15. Создать в окружении переменную name
16. Создать в окружении переменную age
17. Создать в окружении переменную salary
18. Передать в окружение переменную name
	
	pm.environment.set("name", resBody.name);

19. Передать в окружение переменную age
	
	pm.environment.set("age", resBody.age);

20. Передать в окружение переменную salary
	
	pm.environment.set("salary", resBody.salary[0]);

21. Написать цикл который выведет в консоль по порядку элементы списка из параметра salary.
	
	for (a = 0; a < resBody.salary.length; a++){
  	console.log("cycle", resBody.salary[a]);
  	};


				http://162.55.220.72:5005/user_info_2


1. Вставить параметр salary из окружения в request
	salary  {{salary}}

2. Вставить параметр age из окружения в age
	age    {{age}}

3. Вставить параметр name из окружения в name
	name   {{name}}

4. Отправить запрос.
	save -> send

5. Статус код 200
	
	pm.test("Status_code_200", function () {
    	pm.response.to.have.status(200);
	});

6. Спарсить response body в json.
	
	let resBody = pm.response.json();

7. Спарсить request.
	
	let req = request.data;

8. Проверить, что json response имеет параметр start_qa_salary

	pm.test("json_response_имеет_параметр_start_qa_salary", () => {
	pm.expect(resBody).to.have.property("start_qa_salary")});

9. Проверить, что json response имеет параметр qa_salary_after_6_months

	pm.test("json_response_имеет_параметр_qa_salary_after_6_months", () => {
	pm.expect(resBody).to.have.property("qa_salary_after_6_months")});

10. Проверить, что json response имеет параметр qa_salary_after_12_months

	pm.test("json_response_имеет_параметр_qa_salary_after_12_months", () => {
	pm.expect(resBody).to.have.property("qa_salary_after_12_months")});

11. Проверить, что json response имеет параметр qa_salary_after_1.5_year

	pm.test("json_response_имеет_параметр_qa_salary_after_1.5_year", () => {
	pm.expect(resBody).to.have.property("qa_salary_after_1.5_year")
	});

12. Проверить, что json response имеет параметр qa_salary_after_3.5_years

	pm.test("json_response_имеет_параметр_qa_salary_after_3.5_years", () => {
	pm.expect(resBody).to.have.property("qa_salary_after_3.5_years")});

13. Проверить, что json response имеет параметр person

	pm.test("json_response_имеет_параметр_person", () => { 
	pm.expect(resBody).to.have.property("person")});

14. Проверить, что параметр start_qa_salary равен salary из request (salary забрать из request.)

	pm.test("параметр_start_qa_salary_равен_salary_из_request", function () {
	pm.expect(resBody.start_qa_salary).to.eql(1*req.salary)
     }); 

15. Проверить, что параметр qa_salary_after_6_months равен salary*2 из request (salary забрать из request.)

	pm.test("параметр_qa_salary_after_6_months_равен_salary*2_из_request", function () {
	pm.expect(resBody.qa_salary_after_6_months).to.eql(req.salary*2) });

16. Проверить, что параметр qa_salary_after_12_months равен salary*2.7 из request (salary забрать из request.)

	pm.test("параметр_qa_salary_after_12_months_равен_salary*2.7_из_request", function () {
	pm.expect(resBody.qa_salary_after_12_months).to.eql(req.salary*2.7) });

17. Проверить, что параметр qa_salary_after_1.5_year равен salary*3.3 из request (salary забрать из request.)

	pm.test("параметр_qa_salary_after_1.5_year_равен salary*3.3_из_request", function () {
	pm.expect(resBody["qa_salary_after_1.5_year"]).to.eql(req.salary*3.3) });

18. Проверить, что параметр qa_salary_after_3.5_years равен salary*3.8 из request (salary забрать из request.)

	pm.test("Параметр_qa_salary_after_3.5_years_равен salary*3.8_из_request", function () { 
	pm.expect(resBody["qa_salary_after_3.5_years"]).to.eql(req.salary*3.8) }); 

19. Проверить, что в параметре person, 1-й элемент из u_name равен salary из request (salary забрать из request.)

	pm.test("в параметре person, 1-й элемент из u_name равен salary из request", function () {
	pm.expect(resBody.person.u_name[1]).to.eql(req.salary*1) });

20. Проверить, что что параметр u_age равен age из request (age забрать из request.)

	pm.test("параметр u_age равен age из request", function () { 
	pm.expect(resBody.person.u_age).to.eql(+req.age) }); 

21. Проверить, что параметр u_salary_5_years равен salary*4.2 из request (salary забрать из request.)

	pm.test("параметр_u_salary_5_years_равен_salary*4.2_из_request", function () {
	pm.expect(resBody.person.u_salary_5_years).to.eql(req.salary*4.2) }); 

22. ***Написать цикл который выведет в консоль по порядку элементы списка из параметра person.

	for (let a in resBody.person){
	 console.log( a, ":", resBody.person[a]);
     };
