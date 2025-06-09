# API Structure
## course_list
Перелік курсів  

GET: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/course/list
**HTTP Headers**
* Content-Type: application/json  
* X-API-PROVIDER: Zapier  
* X-DRIVED-SECRET: {{bundle.authData.drived_secret}}    

**Значення параметрів:**
* bundle.authData.base_url - адреса відповідної копії DrivEd  
* process.env.API_URL_PREFIX - api/client/v1   
* bundle.authData.drived_secret - API-ключ   

## course_subscribe
Підключення до курсу  

{{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/course/subscribe  
  
**HTTP Headrs**  
* Content-Type: application/json  
* X-API-PROVIDER: Zapier  
* X-DRIVED-SECRET: {{bundle.authData.drived_secret}}  
* Content-Type: application/json  
* Accept: application/json  
**Request Body**  
* email: {{bundle.inputData.email}}  
* course: {{bundle.inputData.course}}  

## course_unsubscribe
Відписка від курсу   

POST: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/course/unsubscribe  
**HTTP Headrs**  
* Content-Type: application/json   
* X-API-PROVIDER: Zapier  
* X-DRIVED-SECRET: {{bundle.authData.drived_secret}}  
* Content-Type: application/json  
* Accept: application/json  
**Request Body**  
* email: {{bundle.inputData.email}}  
* course: {{bundle.inputData.course}}  

## bunch_subscribe  
Підключення до групи  

POST: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/bunch/subscribe  
  
**HTTP Headrs**
* Content-Type: application/json
* X-API-PROVIDER: Zapier
* X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
* Content-Type: application/json
* Accept: application/json  
* 
**Request Body**
* email: {{bundle.inputData.email}}
* course: {{bundle.inputData.course}} 


## bunch_unsubscribe
Відписка від групи

POST: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/bunch/unsubscribe

**HTTP Headrs**
* Content-Type: application/json
* X-API-PROVIDER: Zapier
* X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
* Content-Type: application/json
* Accept: application/json

**Request Body**
* email: {{bundle.inputData.email}}
* bunch: {{bundle.inputData.bunch}}

## Course_Completed_Trigger

Subscribe  

POST: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/zapier/trigger/course  
**HTTP Headrs**  
* Content-Type: application/json
* X-API-PROVIDER: Zapier
* X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
* Content-Type: application/json
* Accept: application/json
  
**Request Body**
* hookUrl: {{bundle.targetUrl}}

**Unsubscribe**
DELETE: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/zapier/trigger/course  
  
**HTTP Headrs**
* Content-Type: application/json
* X-API-PROVIDER: Zapier
* X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
* Content-Type: application/json
* Accept: application/json

**Request Body**  
* hookUrl: {{bundle.targetUrl}}

**Perform List**
GET: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/zapier/trigger/course/samples 
  
**HTTP Headrs**  
* Content-Type: application/json
* X-API-PROVIDER: Zapier
* X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
* Content-Type: application/json
* Accept: application/json

## Lesson Completed Trigger

Subscribe  
POST: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/zapier/trigger/lesson
  
**HTTP Headrs**
* Content-Type: application/json
* X-API-PROVIDER: Zapier
* X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
* Content-Type: application/json
* Accept: application/json

**Request Body**
* hookUrl: {{bundle.targetUrl}}  

**Unsubscribe**
DELETE: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/zapier/trigger/lesson

**HTTP Headrs**  
* Content-Type: application/json
* X-API-PROVIDER: Zapier
* X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
* Content-Type: application/json
* Accept: application/json

**Request Body**
* hookUrl: {{bundle.targetUrl}}

**Perform List**
GET: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/zapier/trigger/lesson/samples

**HTTP Headrs**
* Content-Type: application/json
* X-API-PROVIDER: Zapier
* X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
* Accept: application/json
