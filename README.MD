# Zap Integrations
## Загальний опис додатку.
1. Назва
2. Опис (максимальна довжина 160 символів, мінімальна довжина 40 символів).
3. Домашня сторінка додатку 
4. Логотип (мінімальний розмір 256x256, та бувають особливості по формату. Є вимоги 512x512 або більше, які не включають назву додатку, але на практиці - не застосовується).
5. Цільова аудиторія (для себе або публічна).
6. Роль (працюю на комапанію для розробки інтеграції).
7. Категорія (освіта).

## Authentication
API Key
### Step 1. Configure your Fields
#### API Key
* Label: API Key
* Key: drived_secret
* Required: Yes
* Type: String
* Help Text: [Available on the general settings section]
* Input format: _
* Default value: _
* Static Dropdown: _
#### API Base URL
* Label: API Base URL
* Key: base_url
* Required: Yes
* Type: String
* Help Text: _
* Input format: _
* Default value: [Application adress]
* Static Dropdown: _
### Step 2. Configure a test Request & Connection Label
#### Test
* GET: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/course/list
  *  **HTTP Headers**
     * Content-Type: application/json
     * X-API-PROVIDER: Zapier
     * X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
### Step 3. Test your Autentification
Для тестування вам знадобиться адреса точки входу додатку, та API (Яке знаходиться в пункті меню "налаштування" в додатку: API key).

## Advanced
### Environment Variables
* Key: API_URL_PREFIX | VALUE: api/client/v1
### Request Template
* **HTTP Headers**
  * Content-Type: application/json
  * X-API-PROVIDER: Zapier
  * X-DRIVED-SECRET: {{bundle.authData.drived_secret}}

## Actions
### Assign User to Course Action
#### Settings
* Type: create
* Key: assign_user_to_course
* Name: Assign User to Course
* Noun: Course
* Description: Assign user to course (course id and a user email are required)
* Visibility in Editor: Shown
#### Input Designer
##### Input Field
* Key: email
* Label: Email
* Type: String
* Default Text: _
* Options: Required

##### Dynamic Field
```
const options = {
  url: `${bundle.authData.base_url}/${process.env.API_URL_PREFIX}/course/list`,
  method: 'GET',
  headers: {
    'X-DRIVED-SECRET': bundle.authData.drived_secret,
    'X-API-PROVIDER': bundle.authData.api_provider,
    'Content-Type': 'application/json'
  }
};

return z.request(options)
  .then((response) => {
    const courses = response.json.data;  // Get the array of courses
    
    // Prepare the output object according to your required structure
    return {
      key: 'course',              // Unique key for the dropdown field
      label: 'Course',            // The label shown to users for this input field
      required: true,             // Mark the field as required
      choices: courses.map(course => ({
        label: course.name,       // Shown in the dropdown
        value: course.article     // Value sent when the user selects the course
      }))
    };
  });
```
#### API Configuration
##### Step 1. Configure your API Request 
API Endpoint
* POST: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/course/subscribe
* HTTP Headrs
  * Content-Type: application/json
  * X-API-PROVIDER: Zapier
  * X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
  * Content-Type: application/json
  * Accept: application/json
* Request Body
  * email: {{bundle.inputData.email}}
  * course: {{bundle.inputData.course}}

##### Step 2. Test your API Request 
Test Setup


##### Step 3. Test your API Request 
```
{
  "success": true
}
```
1---------------------2

### Unassign User From Course Action
#### Settings
* Type: create
* Key: unsubscribe_user_from_course
* Name: Unassign User From Course
* Noun: Course
* Description: Unassigns user from a course (course id and a user email are required)
* Visibility in Editor: Shown
#### Input Designer
##### Input Field
* Key: email
* Label: Email
* Type: String
* Default Text: _
* Options: Required

##### Dynamic Field
```
const options = {
  url: `${bundle.authData.base_url}/${process.env.API_URL_PREFIX}/course/list`,
  method: 'GET',
  headers: {
    'X-DRIVED-SECRET': bundle.authData.drived_secret,
    'X-API-PROVIDER': bundle.authData.api_provider,
    'Content-Type': 'application/json'
  }
};

return z.request(options)
  .then((response) => {
    const courses = response.json.data;  // Get the array of courses
    
    // Prepare the output object according to your required structure
    return {
      key: 'course',              // Unique key for the dropdown field
      label: 'Course',            // The label shown to users for this input field
      required: true,             // Mark the field as required
      choices: courses.map(course => ({
        label: course.name,       // Shown in the dropdown
        value: course.article     // Value sent when the user selects the course
      }))
    };
  });
```
#### API Configuration
##### Step 1. Configure your API Request 
API Endpoint
* POST: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/course/unsubscribe
* HTTP Headrs
  * Content-Type: application/json
  * X-API-PROVIDER: Zapier
  * X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
  * Content-Type: application/json
  * Accept: application/json
* Request Body
  * email: {{bundle.inputData.email}}
  * course: {{bundle.inputData.course}}

##### Step 2. Test your API Request 
Test Setup


##### Step 3. Test your API Request 
```
{
  "success": true
}
```
2---------------------3

### Assign User to Group Action
#### Settings
* Type: create
* Key: subscribe_user_to_group
* Name: Assign User to Group
* Noun: Group
* Description: Assignes the user to the selected group
* Visibility in Editor: Shown
#### Input Designer
##### Input Field
* Key: email
* Label: Email
* Type: String
* Default Text: _
* Options: Required

##### Dynamic Field
```
const options = {
  url: `${bundle.authData.base_url}/${process.env.API_URL_PREFIX}/bunch/list`,
  method: 'GET',
  headers: {
    'X-DRIVED-SECRET': bundle.authData.drived_secret,
    'X-API-PROVIDER': bundle.authData.api_provider,
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    limit: "1000000"
  })
};

return z.request(options)
  .then((response) => {
    const bunches = response.json;  // Get the array of groups
    
    // Prepare the output object according to the required structure
    return {
      key:   'bunch',               // Unique key for the dropdown field
      label: 'Group',             // The label shown to users for this input field
      required: true,             // Mark the field as required
      choices: bunches.map(bunch => ({
        label: bunch.name,        // Name shown in the dropdown
        value: bunch.id           // Value sent when the user selects the group
      }))
    };
  });

```
#### API Configuration
##### Step 1. Configure your API Request 
API Endpoint
* POST: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/bunch/subscribe
* HTTP Headrs
  * Content-Type: application/json
  * X-API-PROVIDER: Zapier
  * X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
  * Content-Type: application/json
  * Accept: application/json
* Request Body
  * email: {{bundle.inputData.email}}
  * course: {{bundle.inputData.course}}

##### Step 2. Test your API Request 
Test Setup


##### Step 3. Test your API Request 
```
{
  "success": true
}
```


3---------------------4

### Unassign User From Group Action
#### Settings
* Type: create
* Key: unsubscribe_user_from_group
* Name: Unassign User From Group
* Noun: Group
* Description: Unassigns the user from the selected group
* Visibility in Editor: Shown
#### Input Designer
##### Input Field
* Key: email
* Label: Email
* Type: String
* Default Text: _
* Options: Required

##### Dynamic Field
```
const options = {
  url: `${bundle.authData.base_url}/${process.env.API_URL_PREFIX}/bunch/list`,
  method: 'GET',
  headers: {
    'X-DRIVED-SECRET': bundle.authData.drived_secret,
    'X-API-PROVIDER': bundle.authData.api_provider,
    'Content-Type': 'application/json'
  },
  body: JSON.stringify({
    limit: "1000000"
  })
};

return z.request(options)
  .then((response) => {
    const bunches = response.json;  // Get the array of groups
    
    // Prepare the output object according to the required structure
    return {
      key:   'bunch',               // Unique key for the dropdown field
      label: 'Group',             // The label shown to users for this input field
      required: true,             // Mark the field as required
      choices: bunches.map(bunch => ({
        label: bunch.name,        // Name shown in the dropdown
        value: bunch.id           // Value sent when the user selects the group
      }))
    };
  });


```
#### API Configuration
##### Step 1. Configure your API Request 
API Endpoint
* POST: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/bunch/unsubscribe
* HTTP Headrs
  * Content-Type: application/json
  * X-API-PROVIDER: Zapier
  * X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
  * Content-Type: application/json
  * Accept: application/json
* Request Body
  * email: {{bundle.inputData.email}}
  * bunch: {{bundle.inputData.bunch}}

##### Step 2. Test your API Request 
Test Setup


##### Step 3. Test your API Request 
```
{
  "success": true
}
```


## Trigers
### Course ID Trigger
#### Settings
* Key: course_id
* Name: Course ID
* Noun: Course ID
* Description: Triger to getting data from courses list.
* Directions: _
* Visibility in Editor: Hidden

#### Input Designer

#### API Configuration
##### Step 1. Configure your Request
Trigger Type: Polling

API Endpoint:
```
const options = {
  url: `${bundle.authData.base_url}/${process.env.API_URL_PREFIX}/course/list/`,
  method: 'GET',
  headers: {
    'Accept': 'application/json'
  },
  params: {

  },
  removeMissingValuesFrom: {
    'body': false,
    'params': false
  },
}

return z.request(options)
  .then((response) => {
    const results = response.json.data;

    // You can do any parsing you need for results here before returning them

    return results;
  });
  ```

##### Step 2. Test your API Request
##### Step 3. Define your Output
###### Sample Data
```
{
  "id": "48ee5eef-70aa-e965-62ea-e7942192a2ca",
  "name": "#Corse_1: Level 3",
  "status": 1,
  "article": "6758181f91-1733914038-8813",
  "created_at": "2024-12-11 10:47:18"
}
```
###### Output Field
* id
* name (article)

1-----------2
### Course Completed Trigger
#### Settings
* Key: course_completed
* Name: Course Completed
* Noun: Course
* Description: Triggers when the course is completed.
* Directions: _
* Visibility in Editor: Shown

#### Input Designer
##### Course ID
* Key: course_id
* Name: Course ID
* Help Text: ```Navigate to the course page and click the “Settings” button.
The course ID can be found in the “Basic Information” settings section, next to the “Course ID” label.```

* Type: String
* Options: Required
* Dropdown:
  * Dropdown type:
    * Dynamic
  * Dropdown Source: Course ID
  * Field Name: Id
  * Field Label: Name



#### API Configuration
##### Step 1. Configure your API Request
* Trigger Type: REST Hook
* **Subscribe**
  * POST: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/zapier/trigger/course
    * HTTP Headrs
      * Content-Type: application/json
      * X-API-PROVIDER: Zapier
      * X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
      * Content-Type: application/json
      * Accept: application/json
    * Request Body
      * hookUrl: {{bundle.targetUrl}}
* **Unsubscribe**
  * DELETE: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/zapier/trigger/course
    * HTTP Headrs
      * Content-Type: application/json
      * X-API-PROVIDER: Zapier
      * X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
      * Content-Type: application/json
      * Accept: application/json
    * Request Body
      * hookUrl: {{bundle.targetUrl}}
* **Perform List**
  * GET: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/zapier/trigger/course/samples
    * HTTP Headrs
      * Content-Type: application/json
      * X-API-PROVIDER: Zapier
      * X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
      * Content-Type: application/json
      * Accept: application/json
* **Perform**
  * return [bundle.cleanedRequest];
##### Step 2. Test yor API Request

##### Step 3. Define your Output
```
{
  "userEmail": "student@example.com",
  "userName": "JohnSmith",
  "firstName": "John",
  "lastName": "Smith",
  "courseName": "English"
}
```
2-----------------3
### Course ID Trigger
#### Settings
* Key: course_id
* Name: Course ID
* Noun: Course ID
* Description: Triger to getting data from courses list.
* Directions: _
* Visibility in Editor: Hidden

#### Input Designer

#### API Configuration
##### Step 1. Configure your Request
Trigger Type: Polling

API Endpoint:
```
const options = {
  url: `${bundle.authData.base_url}/${process.env.API_URL_PREFIX}/course/list/`,
  method: 'GET',
  headers: {
    'Accept': 'application/json'
  },
  params: {

  },
  removeMissingValuesFrom: {
    'body': false,
    'params': false
  },
}

return z.request(options)
  .then((response) => {
    const results = response.json.data;

    // You can do any parsing you need for results here before returning them

    return results;
  });
  ```

##### Step 2. Test your API Request
##### Step 3. Define your Output
###### Sample Data
```
{
  "id": "48ee5eef-70aa-e965-62ea-e7942192a2ca",
  "name": "#Corse_1: Level 3",
  "status": 1,
  "article": "6758181f91-1733914038-8813",
  "created_at": "2024-12-11 10:47:18"
}
```
###### Output Field
* id
* name (article)

3---------4
### Lesson Completed Trigger
#### Settings
* Key: lesson_completed
* Name: Lesson Completed
* Noun: Lesson
* Description: Triggers when the lesson is completed.
* Directions: _
* Visibility in Editor: Shown

#### Input Designer
* Key: course_id
* Name: Course
* Help Text: ```Choose course for getting lessons```

* Type: String
* Options: _
* Dropdown:
  * Dropdown type:
    * Dynamic
  * Dropdown Source: Course ID
  * Field Name: Id
  * Field Label: Name

#### API Configuration
##### Step 1. Configure your API Request
* Trigger Type: REST Hook
* **Subscribe**
  * POST: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/zapier/trigger/lesson
    * HTTP Headrs
      * Content-Type: application/json
      * X-API-PROVIDER: Zapier
      * X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
      * Content-Type: application/json
      * Accept: application/json
    * Request Body
      * hookUrl: {{bundle.targetUrl}}
* **Unsubscribe**
  * DELETE: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/zapier/trigger/lesson
    * HTTP Headrs
      * Content-Type: application/json
      * X-API-PROVIDER: Zapier
      * X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
      * Content-Type: application/json
      * Accept: application/json
    * Request Body
      * hookUrl: {{bundle.targetUrl}}
* **Perform List**
  * GET: {{bundle.authData.base_url}}/{{process.env.API_URL_PREFIX}}/zapier/trigger/lesson/samples
    * HTTP Headrs
      * Content-Type: application/json
      * X-API-PROVIDER: Zapier
      * X-DRIVED-SECRET: {{bundle.authData.drived_secret}}
      * Accept: application/json
* **Perform**
  * return [bundle.cleanedRequest];
##### Step 2. Test yor API Request

##### Step 3. Define your Output
```
{
  "userEmail": "student@example.com",
  "userName": "JohnSmith",
  "firstName": "John",
  "lastName": "Smith",
  "courseName": "English"
}
```