# Polly
# Serverless Application for Text-to-Speech Conversion using AWS

This project demonstrates a fully serverless architecture for converting user-submitted posts into audio files using AWS services. The application hosts a static webpage for interacting with the system and utilizes a series of AWS services to process, convert, and store audio files.

---

## Table of Contents

- [Architecture Overview](#architecture-overview)
- [Key AWS Services](#key-aws-services)
- [How It Works](#how-it-works)
- [Setup Instructions](#setup-instructions)
- [Future Enhancements](#future-enhancements)
- [License](#license)

---
## Architecture Diagram
![Architecture Diagram](path/to/your/image/polly.jpeg)


## Architecture Overview

Below is a step-by-step explanation of the architecture:

1. **Static Web Hosting**:  
   - **Amazon S3** is used to host the static content of the web application. This is where users access the front-end of the application.

2. **API Gateway**:  
   - **Amazon API Gateway** acts as the entry point for client requests, providing RESTful endpoints for interaction with the back-end services.

3. **DynamoDB Storage**:  
   - **Amazon DynamoDB** serves as the back-end database for storing the user-submitted posts and their metadata.

4. **New Post Lambda Function**:  
   - A **Lambda function** (`New Post`) is triggered by API Gateway to store new posts in DynamoDB and send a notification to Amazon SNS.

5. **Amazon SNS**:  
   - **Amazon Simple Notification Service (SNS)** decouples the post storage process from the audio conversion process, ensuring scalability and fault tolerance.

6. **Convert to Audio Lambda Function**:  
   - A **Lambda function** (`Convert to Audio`) is triggered by SNS to process the post data and convert text into speech using Amazon Polly.

7. **Text-to-Speech with Amazon Polly**:  
   - **Amazon Polly** converts the text from posts into MP3 audio files.

8. **Audio Storage**:  
   - The generated audio files are stored in **Amazon S3** for retrieval and playback.

9. **Get Post Lambda Function**:  
   - A **Lambda function** (`Get Post`) retrieves post and audio data from DynamoDB and S3, enabling the web application to display the information to users.

---

## Key AWS Services

- **Amazon S3**: Static web hosting and storage for generated MP3 files.
- **Amazon API Gateway**: RESTful API endpoints for interaction.
- **AWS Lambda**: Event-driven serverless functions for business logic.
- **Amazon DynamoDB**: NoSQL database for storing user posts.
- **Amazon SNS**: Message brokering for decoupling processes.
- **Amazon Polly**: Text-to-speech conversion service.

---

## How It Works

1. **User Interaction**:  
   Users access the static webpage hosted on Amazon S3. They can create new posts or view existing posts with audio.

2. **Post Submission**:  
   When a user submits a post:
   - The API Gateway triggers the `New Post` Lambda function.
   - The post data is stored in DynamoDB.
   - A notification is sent to SNS.

3. **Audio Conversion**:  
   - The SNS notification triggers the `Convert to Audio` Lambda function.
   - This function retrieves the post data, uses Amazon Polly to generate an MP3 file, and stores the file in S3.

4. **Post Retrieval**:  
   - When users view posts, the `Get Post` Lambda function fetches data from DynamoDB and S3 for display on the static webpage.

---

## Setup Instructions

1. **AWS Resources**:
   - Create and configure the required AWS services: S3, API Gateway, Lambda, DynamoDB, SNS, and Polly.

2. **Static Web Content**:
   - Upload the front-end application to an S3 bucket configured for static website hosting.

3. **Lambda Functions**:
   - Deploy the `New Post`, `Get Post`, and `Convert to Audio` Lambda functions.
   - Ensure proper IAM roles and permissions are set for these functions.

4. **Database and API Setup**:
   - Configure DynamoDB for post storage.
   - Set up API Gateway to route requests to the Lambda functions.

5. **SNS Integration**:
   - Create an SNS topic for processing notifications and subscribe the `Convert to Audio` function.

---

## Future Enhancements

- Add authentication and authorization using Amazon Cognito.
- Enable real-time updates with AWS AppSync or WebSockets.
- Enhance the front-end with a modern UI framework.

---

## License

This project is licensed under the MIT License. See the LICENSE file for details.
