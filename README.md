# **Trivia App**

## **Udacity API Development and Documentation Final Project**

Udacity is invested in creating bonding experiences for its employees and students. A bunch of team members got the idea to hold trivia on a regular basis and created a webpage to manage the trivia app and play the game.
The application:

1. Display questions - both all questions and by category. 
2. Delete questions.
3. Add questions and require that they include question and answer text.
4. Search for questions based on a text query string.
5. Play the quiz game, randomizing either all questions or within a specific category.

## **Getting Started**

### Pre-requeisites
- Developers using this project should already have Python3, pip, and node installed on their local machines. 
- We recommend working within a virtual environment for this project. This keeps your dependencies for each project separate and organized. Instructions for setting up a virual environment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

### **Set up the Backend**

**PIP Dependencies** - Once your virtual environment is setup and running, install the required dependencies by navigating to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

#### Key Pip Dependencies

- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use to handle the lightweight SQL database. You'll primarily work in `app.py`and can reference `models.py`.

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross-origin requests from our frontend server.

### **Set up the Database**

With Postgres running, create a `trivia` database:

```bash
createdb trivia
```

Populate the database using the `trivia.psql` file provided. From the `backend` folder in terminal run:

```bash
psql trivia < trivia.psql
```

### **Run the Server**

From within the `./src` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
flask run --reload
```

The `--reload` flag will detect file changes and restart the server automatically.


### **Set up the Frontend**

> _tip_: this frontend is designed to work with [Flask-based Backend](../backend) so it will not load successfully if the backend is not working or not connected. We recommend that you **stand up the backend first**, test using Postman or curl, update the endpoints in the frontend, and then the frontend should integrate smoothly.

#### Installing Dependencies

1. **Installing Node and NPM**
   This project depends on Nodejs and Node Package Manager (NPM). Before continuing, you must download and install Node (the download includes NPM) from [https://nodejs.com/en/download](https://nodejs.org/en/download/).

2. **Installing project dependencies**
   This project uses NPM to manage software dependencies. NPM Relies on the package.json file located in the `frontend` directory of this repository. After cloning, open your terminal and run:

```bash
npm install
```

> _tip_: `npm i`is shorthand for `npm install``


#### **Running Your Frontend**

The frontend app was built using create-react-app. In order to run the app in development mode use `npm start`. You can change the script in the `package.json` file.

Open [http://localhost:3000](http://localhost:3000) to view it in the browser. The page will reload if you make edits.

```bash
npm start
```

## **API Reference**

### **Getting Started**
- Base URL: At present this app can only be run locally and is not hosted as a base URL. The backend app is hosted at the default, http://127.0.0.1:5000

## Endpoints

#### `GET '/categories'`
- General
   - Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category
   - Request Arguments: None
   - Returns: An object with a single key, categories, that contains an object of id: category_string key:value pairs.
- Sample: 
  - Request: 
  `curl http://127.0.0.1:5000/categories`
  - Response:

    ```JSON
    {
    "categories": {
        "1": "Science",
        "2": "Art",
        "3": "Geography",
        "4": "History",
        "5": "Entertainment",
        "6": "Sports"
    },
    "success": true,
    }
    ```

#### `GET '/questions?page=${integer}'`
- General
  - Fetches a paginated set of questions, a total number of questions, all categories and current category string.
  - Request Arguments: `page` - integer (optional)
  - Returns: An object with 10 paginated questions, total questions, object including all categories, and current category string
- sample 
  - Request: `curl http://127.0.0.1:5000/questions`
  - Response:
    ```JSON
    {
        categories: {
            1: "Science",
            2: "Art",
            3: "Geography",
            4: "History",
            5: "Entertainment",
            6: "Sports"
        },
        currentCategory: "Geography",
        questions: [
            {
                answer: "Apollo 13",
                category: 5,
                difficulty: 4,
                id: 2,
                question: "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
            },
            {
                answer: "Tom Cruise",
                category: 5,
                difficulty: 4,
                id: 4,
                question: "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
            },
            {
                answer: "Maya Angelou",
                category: 4,
                difficulty: 2,
                id: 5,
                question: "Whose autobiography is entitled 'I Know Why the Caged Bird Sings'?"
            },
            {
                answer: "Edward Scissorhands",
                category: 5,
                difficulty: 3,
                id: 6,
                question: "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
            },
            {
                answer: "Muhammad Ali",
                category: 4,
                difficulty: 1,
                id: 9,
                question: "What boxer's original name is Cassius Clay?"
            },
            {
                answer: "Brazil",
                category: 6,
                difficulty: 3,
                id: 10,
                question: "Which is the only team to play in every soccer World Cup tournament?"
            },
            {
                answer: "Uruguay",
                category: 6,
                difficulty: 4,
                id: 11,
                question: "Which country won the first ever soccer World Cup in 1930?"
            },
            {
                answer: "George Washington Carver",
                category: 4,
                difficulty: 2,
                id: 12,
                question: "Who invented Peanut Butter?"
            },
            {
                answer: "Lake Victoria",
                category: 3,
                difficulty: 2,
                id: 13,
                question: "What is the largest lake in Africa?"
            },
            {
                answer: "The Palace of Versailles",
                category: 3,
                difficulty: 3,
                id: 14,
                question: "In which royal palace would you find the Hall of Mirrors?"
            }
        ],
        success: true,
        totalQuestions: 19
    }
    ```

#### `GET '/categories/<int:category_id>/questions'`
- General
  - Returns questions for a cateogry specified by id request argument.
  - Request Arguments: `category_id` - integer
  - Returns: An object with questions for the specified category, total questions, and current category string
- Sample 
  - Request: `curl http://127.0.0.1:5000/categories/2/questions`
  - Response:

    ```JSON
    {
    "currentCategory": "Art",
    "questions": [
        {
        "answer": "Escher",
        "category": 2,
        "difficulty": 1,
        "id": 16,
        "question": "Which Dutch graphic artist\u2013initials M C was a creator of optical illusions?"
        },
        {
        "answer": "Mona Lisa",
        "category": 2,
        "difficulty": 3,
        "id": 17,
        "question": "La Giaconda is better known as what?"
        },
        {
        "answer": "One",
        "category": 2,
        "difficulty": 4,
        "id": 18,
        "question": "How many paintings did Van Gogh sell in his lifetime?"
        },
        {
        "answer": "Jackson Pollock",
        "category": 2,
        "difficulty": 2,
        "id": 19,
        "question": "Which American artist was a pioneer of Abstract Expressionism, and a leading exponent of action painting?"
        }
    ],
    "success": true,
    "totalQuestions": 4
    }

    ```


#### `DELETE '/questions/<int:question_id>'`
- General
  - Deletes a specified question using the id of the question.
  - Request Arguments: `question_id` (required)
  - Returns: deleted object id and success
- Sample 
  - Request: `curl -X DELETE http://127.0.0.1:5000/questions/2`
  - Response:

    ```JSON
    {
    "deleted": 2,
    "success": true
    }
    ```

#### `POST '/questions'`
- General
  - Sends a post request in order to add a new question
  - Request Arguments: a key/value pairs object whit the following content:
    - `question`: string containing the question itself.
    - `answer`: answer's string.
    - `difficulty`: difficulty level.
    - `category`: category ID field.
  - Returns: created question id, total questions, message of status code, status code, and success value
- Sample
  - Request:  
   `curl -X POST http://127.0.0.1:5000/questions -H 'Content-Type: application/json' -d '{"question": "What does ORM stands for?", "answer" : "Object Relation Mapping", "difficulty": "1", "category": "1"}'
`
  - Response

    ```JSON
    {
        "createdQuestion": 24,
        "message": "created",
        "success": true,
        "totalQuestions": 19
    }
    ```

#### `POST '/search'`
- General
    - Sends a post request in order to search for a specific question by search term
    - Request Arguments:
        - `searchTerm`: string to search in questions string.
    - Returns: any array of questions, a number of totalQuestions that met the search term and the current category string

- Sample:
  - Request: `curl -X POST http://127.0.0.1:5000/search -H 'Content-Type: application/json' -d '{"searchTerm": "orm"}'`
  - Response: 

    ```JSON
    {
    "currentCategory": "Science",
    "questions": [
        {
        "answer": "Object Relation Mapping",
        "category": 1,
        "difficulty": 1,
        "id": 24,
        "question": "What does ORM stands for?"
        }
    ],
    "success": true,
    "totalQuestions": 1
    }
    ```


#### `POST '/quizzes'`
- General
    - Sends a post request in order to get the next question
    - Request Arguments:
        - `category_id`: question's category id field.
        - `previous_quesion`: question in the previous iteration, first time it's an empty string.
    - Returns: a single new question object

- Samplel
```JSON
{
  "question": {
    "answer": "Alexander Fleming",
    "category": 1,
    "difficulty": 3,
    "id": 21,
    "question": "Who discovered penicillin?"
  },
  "success": true
}
```

## Errors handling:
All endpoints are provided with error handlers functions which return the following key/value pairs JSON content:
- `success`: False.
- `error`: error code number.
- `message`: error message string giving a brief description of the kind of error.

Here is an example of the returned object:

```JSON
{
    "success": False,
    "error": 404,
    "message": "Resource Not Found"
}
```


