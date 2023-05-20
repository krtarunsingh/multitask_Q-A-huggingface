# multitask_Q-A-huggingface
In this task, I developed an API for question answering using a question classification model, information retrieval, answer generation, and answer validation. The API follows RESTful principles and accepts a question as input, retrieves relevant information, generates a potential answer, and validates the answer before returning it as output.



API Documentation:


### Endpoint: /api/answer

This endpoint accepts a POST request with a JSON payload containing a question and a context. It returns a JSON response with a validated answer based on the question and context provided.

#### Request

- Method: POST
- Content-Type: application/json

##### Request Body

The request body should be a JSON object with the following fields:

- `question` (string): The question to be answered.
- `context` (string): The context or information related to the question.

Example request body:
```json
{
  "question": "What is the sales department responsible for?",
  "context": "The sales department is responsible for handling the sales operations of the company. They manage client relationships, negotiate deals, and meet sales targets."
}
```

#### Response

##### Response Body

The response body will be a JSON object with the following fields:

- `question` (string): The question received in the request.
- `context` (string): The context received in the request.
- `answer` (string): The generated answer based on the question and context.
- `answer_present` (boolean): Indicates whether the generated answer is present in the context (true or false).
- `answer_contains_keywords` (boolean): Indicates whether the generated answer contains keywords related to the question (true or false).

Example response body:
```json
{
  "question": "What is the sales department responsible for?",
  "context": "The sales department is responsible for handling the sales operations of the company. They manage client relationships, negotiate deals, and meet sales targets.",
  "answer": "handling the sales operations of the company",
  "answer_present": true,
  "answer_contains_keywords": true
}
```

##### HTTP Status Codes

- 200 OK: The request was successful, and the response body contains the validated answer.
- 400 Bad Request: The request is invalid or missing required fields in the request body.

#### Example

##### Request

```
POST /api/answer
Content-Type: application/json

{
  "question": "What is the sales department responsible for?",
  "context": "The sales department is responsible for handling the sales operations of the company. They manage client relationships, negotiate deals, and meet sales targets."
}
```

##### Response

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "question": "What is the sales department responsible for?",
  "context": "The sales department is responsible for handling the sales operations of the company. They manage client relationships, negotiate deals, and meet sales targets.",
  "answer": "handling the sales operations of the company",
  "answer_present": true,
  "answer_contains_keywords": true
}
```

This API allows you to send a question and context, and it responds with a validated answer based on the provided information. You can use this API to integrate question-answering functionality into your applications or services.

Please note that the provided documentation is just an example, and you can customize it according to your specific API requirements, including additional details, error handling, authentication, and any other necessary information.




### Breif Details of the Approach:
In this task, I developed an API for question answering using a question classification model, information retrieval, answer generation, and answer validation. The API follows RESTful principles and accepts a question as input, retrieves relevant information, generates a potential answer, and validates the answer before returning it as output.

Models Used:
1. Question Classification: I used Hugging Face's 'distilbert-base-uncased' model, fine-tuned on a question classification task. This model categorizes the input question into different categories such as "Company Department", "Employee Role", "Company News", etc.

2. Answer Generation: For generating potential answers, I utilized Hugging Face's 'bert-large-uncased-whole-wordmasking-finetuned-squad' model. This model is pre-trained on the Stanford Question Answering Dataset (SQuAD) and is capable of generating answers based on the given context and question.

Logic Behind the Architecture:
1. Question Classification: The API starts by analyzing and categorizing the input question using the question classification model. This helps in determining the type of information to retrieve.

2. Information Retrieval: Depending on the question category, the API retrieves relevant information. This can involve querying an SQL database for employee details, making requests to a news API for company news, or fetching information from a CSV file for departmental details.

3. Answer Generation: Once the relevant information is retrieved, the API generates a potential answer using the answer generation model. The model takes the question and retrieved information as context and predicts the answer.

4. Answer Validation: The generated answer is then validated to ensure its correctness. This involves checking if the answer is present in the retrieved context and if it contains any keywords related to the question. These validation mechanisms help in ranking and filtering the potential answers.

Challenges Faced and Solutions:
1. Model Selection: Choosing the right models for question classification and answer generation was crucial. I selected pre-trained models fine-tuned on relevant tasks to ensure accurate results.

2. Data Availability: Acquiring and preparing relevant datasets for fine-tuning the models can be challenging. I relied on publicly available datasets and existing pre-trained models to overcome this challenge.

3. Integration and Deployment: Integrating the various components and deploying the API can be complex. I utilized Flask, a popular web framework, to handle API requests and responses, and ensured the API followed RESTful principles.

4. Answer Validation: Validating the generated answer required implementing logic to check for answer presence and keyword matching. I used regular expressions and string matching techniques to perform answer validation effectively.

Overall, the approach involved using pre-trained models for question classification and answer generation, retrieving information based on the question category, and validating the generated answers. The API architecture followed RESTful principles and incorporated the necessary components for question answering.
