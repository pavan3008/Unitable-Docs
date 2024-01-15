
# System Architecture Documentation

## Overview

This document outlines the server architecture for a recommendation engine, detailing the interaction between various components including databases, caches, and APIs. The system's primary function is to generate and retrieve recommendations based on user queries.

## Components

### PostgreSQL

*Purpose*: Serves as the primary relational database for storing persistent data.

*Interaction*: PostgreSQL stores user data and recommendation logic that can be retrieved during the recommendation generation process.

### Redis Cache

*Purpose*: Provides fast access to frequently used data through in-memory storage.

*Interaction*: Temporarily caches user IDs and corresponding responses to improve performance and reduce load on the primary database.

### MongoDB

*Purpose*: Stores non-relational data such as recommendation history and logs.

*Interaction*: Acts as a datastore for logging all recommendation requests and responses for analytical purposes.

### REST API

*Purpose*: Interface for client-server communication, handling user requests and responses.

*Interaction*: Processes incoming requests, interacts with the token generation for authentication, communicates with Redis Cache, and initiates recommendation retrieval.

- **Fetch Recommendations API** 
- **Venue API**

### Token Generation

*Purpose*: Manages user authentication and session tokens.

*Interaction*: Generates unique user tokens to validate session authenticity and to track recommendation requests.

## RAG Pipeline

*Purpose*: Represents the Retrieval-Augmentation-Generation process for recommendations.

*Interaction*: Orchestrates the workflow for fetching, enhancing, and generating user-specific recommendations.

### Output Processor

*Purpose*: Formats the API response.

*Interaction*: Takes the raw data from the recommendation engine and formats it according to the API specifications before sending it to the user.

## System Architecture Diagram
https://drive.google.com/file/d/14SwdDBct-V9er2L9xiV5MTmgrKQ8ZR8j/view

## Data Flow

1. *Client Request*: The user initiates a request to the server via the REST API.
2. *Token Validation*: The REST API interacts with the token generation service to authenticate the request.
3. *Data Retrieval*: Depending on the cache status, the request is routed to either Redis Cache or the PostgreSQL database.
4. *RAG Pipeline*: The recommendation logic is processed through the RAG pipeline to generate a tailored recommendation.
5. *Data Storage*: The recommendation and user interaction are logged into MongoDB for tracking and analytical purposes.
6. *Response Formatting*: The output processor formats the recommendation data.
7. *Client Response*: The REST API sends the formatted recommendation back to the client.

## Error Handling

The system has robust error handling at each component level to ensure stability and to provide meaningful feedback to the user in case of failure.

## Scalability and Performance
Each component is designed to scale horizontally to handle increased load. The use of Redis Cache and asynchronous processing ensures high performance and low latency.

## Security Measures
The system implements industry-standard security practices including encrypted tokens, secure data transfer, and regular audits to protect user data and system integrity.

# Enchancements

## Backend:

## Fetch Recommendations API Modification

The Fetch Recommendations API should be updated to include percentage matches. This involves modifying the algorithm to calculate these matches. Below is a guide on how to achieve this:

### Calculation of Percentage Matches
- Define the criteria for matching.
- Assign weights to each criterion based on its importance.
- Compare user preferences with available options.
- Calculate a percentage match using the weighted criteria.

### Algorithm Building
1. Define the input parameters (user preferences and available options).
2. Implement the matching algorithm using the defined criteria and weights.
3. Test the algorithm with various scenarios to ensure accuracy.
4. Optimize the algorithm for efficiency and computational performance.

## Venue Bonni API Modification

Consider revamping the Venue Bonni API. Evaluate the current functionality and make necessary improvements. This may involve enhancing performance, updating features, and ensuring compatibility with the overall system.

## Small LMs Optimization

To optimize the use of Small LMs (Language Models):
- Evaluate the need for using smaller LMs instead of Open AI.
- Consider alternatives for more efficiency and computational optimization.
- Implement LlamaV2 or LangChain for better performance.

## Frontend:

### Native or Multiplatform?

Decide whether to develop the frontend using native frameworks (e.g., Swift for iOS, Kotlin for Android) or opt for a multiplatform solution (e.g., Flutter, React Native). Consider factors such as development speed, performance, and platform-specific requirements.

# Questions

## Guests Chatbot

- The initial implementation is a closed-ended chatbot. Decide on the approach for user interactions. Consider making it more sophisticated and controlled, especially if users may not provide all information in a single message.

## Tech Stack for Mobile App

- Define the technology stack for the mobile app. Consider frameworks, programming languages, and tools suitable for mobile development.

## 95% Match Criteria

- Clarify whether the 95% match criteria are sourced from a third party or if Unitable is responsible for determining the match percentage. Determine if any additional algorithms need to be developed after initial messages to achieve the specified match percentage.

**Additional Questions to be discussed*
