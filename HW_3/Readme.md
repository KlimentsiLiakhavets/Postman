                                        HW_3 Postman
```
			http://162.55.220.72:5005/login

POST
1) необходимо залогиниться POST

	login : Klim
	password : 123

2) Приходящий токен необходимо передать во все остальные запросы

	let jsonData = pm.response.json();
	pm.environment.set("token", jsonData.token);


			http://162.55.220.72:5005/user_info

req. (RAW JSON)
POST
	{
	  "age":39,
	  "salary":500,
	  "name":"Klim",
	  "auth_token":"{{token}}"
	}

1) Статус код 200

	pm.test("Status code is 200", function () {
    	pm.response.to.have.status(200);
	});

2) Проверка структуры json в ответе

const schemajson = {
    "type": "object",
  "properties": {
    "person": {
      "type": "object",
      "properties": {
        "u_age": {
          "type": "integer"
        },
        "u_name": {
          "type": "array",
          "items": [
            {
              "type": "string"
            },
            {
              "type": "integer"
            },
            {
              "type": "integer"
            }
          ]
        },
        "u_salary_1_5_year": {
          "type": "integer"
        }
      },
      "required": [
        "u_age",
        "u_name",
        "u_salary_1_5_year"
      ]
    },
    "qa_salary_after_12_months": {
      "type": "number"
    },
    "qa_salary_after_6_months": {
      "type": "integer"
    },
    "start_qa_salary": {
      "type": "integer"
    }
  },
  "additionalProperties": false
}
	pm.test("Проверка структуры json в ответе", () => {
	pm.response.to.have.jsonSchema(schemajson);
	});

3) В ответе указаны коэффициенты умножения salary, напишите тесты по проверке 
   правильности результата перемножения на коэффициент.

	let resBody = pm.response.json();
	let reqBody = JSON.parse(request.data);

			Проверка salary в console.

	console.log("salary_from respons = " + resBody.start_qa_salary);
	console.log("salary_from request = " + reqBody.salary);

 			salary_after_6_months равен salary*2 из request.

	pm.test("salary_after_6_months равен salary*2 из request", function () { 
	pm.expect(resBody.qa_salary_after_6_months).to.eql(reqBody.salary*2);
	});

			salary_after_12_months равен salary*2.9 из request.

	pm.test("salary_after_12_months равен salary*2.9 из request", function () { 
	pm.expect(resBody.qa_salary_after_12_months).to.eql(reqBody.salary*2.9);
	});

			salary_after_1.5_year равен salary*4 из request.
	pm.test("salary_after_1.5_year равен salary*4 из request", function () {
	pm.expect(resBody.person.u_salary_1_5_year).to.eql(reqBody.salary*4);
	});

4) Достать значение из поля 'u_salary_1.5_year' и передать в поле salary 
   запроса http://162.55.220.72:5005/get_test_user

	pm.environment.set("u_salary_1_5_year", resBody.person.u_salary_1_5_year);


				http://162.55.220.72:5005/new_data

POST
request	
	  age		{{age}}
	  salary	{{salary}}
	  name		{{name}}
	  auth_token	{{token}}

response 
 	{
    	 "age": 39,
    	 "name": "Klim",
      	 "salary": [
      	  500,
      	 "1000",
         "1500"
    	]
	}

1) Статус код 200

	pm.test("Status code is 200", function () {
   	pm.response.to.have.status(200);
	});

2) Проверка структуры json в ответе

const schemajson = {
  "type": "object",
  "properties": {
    "age": {
      "type": "integer"
    },
    "name": {
      "type": "string"
    },
    "salary": {
      "type": "array",
      "items": [
        {
          "type": "integer"
        },
        {
          "type": "string"
        },
        {
          "type": "string"
        },
      ]
    },
  },
	"additionalProperties": false
}
	pm.test("Проверка структуры json в ответе", () => {
	pm.response.to.have.jsonSchema(schemajson);
	});

3) В ответе указаны коэффициенты умножения salary, напишите тесты по проверке
   правильности результата перемножения на коэффициент.

	let resBody = pm.response.json();
	let salary_1 = resBody.salary[0];
	let salary_2 = +resBody.salary[1];
	let salary_3 = +resBody.salary[2];
	let reqBody = request.data;

	pm.test("Checksum_salary_1", function(){
 	pm.expect(salary_1).to.eql(+reqBody.salary);
 	});

	pm.test("Checksum_salary_2", function(){
 	pm.expect(salary_2).to.eql(reqBody.salary*2);
 	});

	pm.test("Checksum_salary_3", function(){
 	pm.expect(salary_3).to.eql(reqBody.salary*3);
 	});

4) проверить, что 2-й элемент массива salary больше 1-го и 0-го

	pm.test("Прверка, что 2-й элемент массива salary больше 0-го", () => { 
	pm.expect(salary_3).to.be.above(salary_1);
	});

	pm.test("Прверка, что 2-й элемент массива salary больше 1-го", () => {
 	pm.expect(salary_3).to.be.above(salary_2);
	});


			http://162.55.220.72:5005/test_pet_info


POST
request	
	  age		{{age}}
	  weight	98
	  name		{{name}}
	  auth_token	{{token}}

response 
	{
    	  "age": 39,
    	  "daily_food": 1.176,
    	  "daily_sleep": 245.0,
    	  "name": "Klim"
	}

1) Статус код 200

	pm.test("Status code is 200", function () {
    	pm.response.to.have.status(200);
	});

2) Проверка структуры json в ответе

    const schemajson = {
	"type": "object",
  	"properties": {
    	"age": {
      	"type": "integer"
   	},
    	"daily_food": {
    	"type": "number"
    	},
    	"daily_sleep": {
    	"type": "number"
    	},
    	"name": {
      	"type": "string"
    	}
  	},
  	"additionalProperties": false
	}
	pm.test("Проверка структуры json в ответе", () => {
	pm.response.to.have.jsonSchema(schemajson);
	});

3) В ответе указаны коэффициенты умножения weight, напишите тесты по проверке 
   правильности результата перемножения на коэффициент

	let resBody = pm.response.json();
	let reqWeight = request.data.weight;
проверка weight
	console.log("weight из request = " +reqWeight);

	pm.test("Проверка_значения - daily_food = 1.76", function(){
 	pm.expect(resBody.daily_food).to.eql(reqWeight*0.012) 
 	// 98 * 0.012 = 1.76
	});

	pm.test("Проверка_значения - daily_sleep = 245.0", function(){
 	pm.expect(resBody.daily_sleep).to.eql(reqWeight*2.5) 
 	// 98 * 2.5 = 245
	});


 			http://162.55.220.72:5005/get_test_user
	
POST
request
	age		{{age}}
	salary		{{u_salary_1_5_year}}
	name		{{name}}
	auth_token	{{token}}

response
	{
    		"age": "39",
    		"family": {
       		"children": [
            [
                "Alex",
                24
            ],
            [
                "Kate",
                12
            ]
        ],
        	"u_salary_1_5_year": 8000
   	 },
    		"name": "Klim",
   		 "salary": 2000
	}

1) Статус код 200

	pm.test("Status code is 200", function () {
    	pm.response.to.have.status(200);
	});

2) Проверка структуры json в ответе

	const schemajson = {
    "type": "object",
  "properties": {
    "age": {
      "type": "string"
    },
    "family": {
      "type": "object",
      "properties": {
        "children": {
          "type": "array",
          "items": [
            {
              "type": "array",
              "items": [
                {
                  "type": "string"
                },
                {
                  "type": "integer"
                }
              ]
            },
            {
              "type": "array",
              "items": [
                {
                  "type": "string"
                },
                {
                  "type": "integer"
                }
              ]
            }
          ]
        },
        "u_salary_1_5_year": {
          "type": "integer"
        }
      },
      "required": [
        "children",
        "u_salary_1_5_year"
      ]
    },
    "name": {
      "type": "string"
    },
    "salary": {
      "type": "integer"
    }
  },
  "required": [
    "age",
    "family",
    "name",
    "salary"
  ],
    "additionalProperties": false
 }
	pm.test("Проверка структуры json в ответе", () => {
	pm.response.to.have.jsonSchema(schemajson);
	});

3) Проверить что занчение поля name = значению переменной name из окружения

	let name_поля = request.data.name;
	let name_environment = pm.environment.get('name');
		
		проверка в console

	console.log("name_поля = ",name_поля);
	console.log("name_environment = ", name_environment);

	pm.test("name_поля = name_environment", function(){
 	pm.expect(name_поля).to.eql(name_environment);
	});

4) Проверить что занчение поля age в ответе соответсвует отправленному в запросе 
   значению поля age

	let resBody = pm.response.json();
	let age = request.data.age;

	pm.test("request.age = response.age", function(){
	pm.expect(resBody.age).to.eql(age);
	});
 		проверка в console

	console.log("значение_поля_age_с_запроса = ", age);
	console.log("значение_поля_age_в_ответе = ",resBody.age);


			http://162.55.220.72:5005/currency


POST
request
	auth_token	{{token}}

response
	Передаётся список массив объектов
	
1) Можете взять любой объект из присланного списка, используйте js random.
   В объекте возьмите Cur_ID и передать через окружение в следующий запрос.

	let resBody = pm.response.json();
	let cur = resBody.length;
	function randomnoe_ob(cur) { return Math.floor(Math.random() * cur);}
	let random = resBody[randomnoe_ob(cur)];
		Проверка произвольного Cur_ID в объекте в console
	console.log("Произвольное_Cur_ID = ", random['Cur_ID']); 
		Передача в окружение произвольного Cur_ID
	pm.environment.set("Cur_ID",random['Cur_ID']); 


			http://162.55.220.72:5005/curr_byn

POST
request
	auth_token	{{token}}
	curr_code	{{Cur_ID}}

response
	{
    "Cur_Abbreviation": str
    "Cur_ID": int,
    "Cur_Name": str,
    "Cur_OfficialRate": float,
    "Cur_Scale": int,
    "Date": str
	}

1) Статус код 200

	pm.test("Status code is 200", function () {
    	pm.response.to.have.status(200);
	});

2) Проверка структуры json в ответе

	const schemajson = {
    "type": "object",
  "properties": {
    "Cur_Abbreviation": {
      "type": "string"
    },
    "Cur_ID": {
      "type": "integer"
    },
    "Cur_Name": {
      "type": "string"
    },
    "Cur_OfficialRate": {
      "type": "number"
    },
    "Cur_Scale": {
      "type": "integer"
    },
    "Date": {
      "type": "string"
    }
  },
  "required": [
    "Cur_Abbreviation",
    "Cur_ID",
    "Cur_Name",
    "Cur_OfficialRate",
    "Cur_Scale",
    "Date"
  ],
  "additionalProperties": false
}
	pm.test("Проверка структуры json в ответе", () => { 
	pm.response.to.have.jsonSchema(schemajson);
	});
