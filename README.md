
# Generative AI Chatbot Monitoring with MLflow

**Generative AI | LLM Monitoring | Experiment Tracking | Python | OpenAI API | MLflow**

## Project Overview

This project was developed as part of my DSC 670 Generative AI coursework at Bellevue University.

I built an interactive chatbot using Python and OpenAI's API, then integrated MLflow to track its operational performance.

The objective was to understand how monitoring can help evaluate a generative AI application beyond simply checking whether it produces a response.

I recorded response latency, token usage, and model configuration across several chatbot requests, then compared the results to identify performance differences.

## Project Objectives

- Build a functional chatbot using the OpenAI API.
- Connect the application to an MLflow tracking server.
- Record model parameters and performance metrics.
- Compare chatbot requests with different levels of complexity.
- Visualize response latency.
- Troubleshoot experiment tracking issues.
- Create an interactive chatbot that records additional MLflow runs.

## Tools and Technologies

- Python
- JupyterLab
- OpenAI API
- GPT-4o-mini
- MLflow
- Pandas
- Matplotlib
- Tiktoken
- Prometheus Client
- Colorama

## Model Configuration

The chatbot uses OpenAI's `gpt-4o-mini` model.

The experiment was configured with the following settings:

| Parameter | Value |
|---|---|
| Model | `gpt-4o-mini` |
| Temperature | 0.7 |
| Top-p | 1 |
| Frequency penalty | 0 |
| Presence penalty | 0 |
| Maximum completion tokens | 800 |

These settings were recorded in MLflow to provide context for the performance measurements.

## Methodology

### 1. Environment Setup

I verified that the required Python libraries were available in my JupyterLab environment.

I then started a local MLflow tracking server and connected the notebook to it using the following tracking URI:

`http://127.0.0.1:5000`

The experiment was named:

`DSC_670_Week_9_MLflow`

### 2. Chatbot Development

I configured an OpenAI client and created a Python function to send conversation messages to the model.

The function returns the generated response while measuring how long the API request takes.

The API key is obtained from an environment variable or entered securely through a password prompt rather than being written directly into the notebook.

### 3. MLflow Integration

Each chatbot request creates an MLflow run named `Chatbot_Request`.

The application records the following metrics:

- Request count
- Response latency
- Prompt tokens
- Completion tokens
- Total conversation tokens

It also records the model name and generation settings.

This makes it possible to inspect individual requests and compare their operational characteristics.

### 4. Chatbot Testing

I evaluated the chatbot using three prompts:

1. What is machine learning?
2. Explain the difference between supervised and unsupervised learning.
3. Explain how a business could use machine learning to predict customer churn, including the data needed and possible challenges.

These prompts provided a small comparison of requests with different response requirements.

### 5. Performance Visualization

I retrieved the experiment results using MLflow and organized them into a Pandas DataFrame.

I also created a Matplotlib bar chart comparing response times across the three requests.

### 6. Interactive Chatbot

After the initial tests, I added an interactive conversation loop.

Users can enter questions, receive model-generated responses, and continue the conversation until they enter an exit command.

Each successful API request is also recorded through the MLflow tracking function.

## Experiment Results

| Test | Response Time | Prompt Tokens | Completion Tokens | Total Tokens |
|---|---:|---:|---:|---:|
| Test 1 | 5.66 seconds | 22 | 382 | 404 |
| Test 2 | 5.52 seconds | 28 | 489 | 517 |
| Test 3 | 9.46 seconds | 38 | 800 | 838 |

### Key Findings

**Response time varied across requests.**

The first two requests completed in approximately 5.66 and 5.52 seconds, despite using different numbers of tokens.

The third request took approximately 9.46 seconds and used the most tokens.

**More tokens did not always mean a slower response.**

Test 2 used more tokens than Test 1 but completed slightly faster.

This demonstrated why request performance should be measured rather than assumed.

**The longest response reached the configured token limit.**

Test 3 generated exactly 800 completion tokens, matching the maximum setting.

This raised the possibility that the response could be truncated when the model reaches the configured output limit.

**Three requests are not enough to establish a reliable performance pattern.**

Network conditions, response length, and other factors can influence latency.

A larger experiment would be needed before drawing broader conclusions.

## Troubleshooting MLflow Tracking

During development, an initial chatbot request completed successfully, but its metrics did not appear in the expected MLflow dashboard.

I investigated the tracking configuration and discovered that the run had been recorded in a local SQLite database rather than the intended MLflow server.

After locating the original run, I corrected the tracking connection and confirmed that subsequent experiments were recorded in the expected location.

This experience demonstrated an important monitoring lesson:

An application can function correctly while its monitoring data is being recorded somewhere unexpected.

The notebook includes the original troubleshooting steps. Any local file paths shown there are specific to the development environment and should be replaced when reproducing the project.

## What I Learned

This project strengthened my understanding of how to monitor generative AI applications.

I learned how to:

- Track individual chatbot requests using MLflow.
- Record model parameters and operational metrics.
- Compare latency and token usage.
- Retrieve experiment results for analysis.
- Visualize performance differences.
- Diagnose incorrect experiment tracking configurations.
- Maintain conversation history in an interactive chatbot.

Most importantly, I learned that generating a useful response and operating efficiently are separate considerations.

A chatbot may produce helpful answers while still having performance, cost, or monitoring limitations.

## Limitations

- Only three prompts were used for the main performance comparison.
- Response times may vary with network conditions and API service performance.
- The experiment did not measure factual accuracy or response helpfulness.
- Token usage was recorded, but monetary cost was not calculated.
- The project uses a local MLflow tracking server rather than a production monitoring environment.
- The notebook requires an active OpenAI API account and available API usage.

## Future Improvements

- Evaluate a larger collection of prompts.
- Compare multiple OpenAI models.
- Measure the effect of different temperature and token settings.
- Track failed requests and API errors.
- Estimate API costs from token usage.
- Evaluate response accuracy and relevance.
- Study token usage across longer conversations.
- Develop a dashboard for monitoring chatbot performance over time.

## How to Run the Project

### Requirements

- Python and JupyterLab
- An OpenAI API key with available API usage
- MLflow
- OpenAI Python SDK
- Pandas
- Matplotlib
- Tiktoken
- Prometheus Client
- Colorama

### Installation

Install the primary dependencies:

```bash
pip install mlflow openai pandas matplotlib tiktoken prometheus-client colorama
```

### Start MLflow

Open a terminal and start a local MLflow tracking server:

```bash
mlflow server --host 127.0.0.1 --port 5000
```

Keep the server running while executing the notebook.

Open the MLflow dashboard at:

`http://127.0.0.1:5000`

### Run the Notebook

1. Download the notebook from this repository.
2. Open it in JupyterLab.
3. Start the MLflow tracking server.
4. Run the environment setup and tracking configuration cells.
5. Provide your OpenAI API key when prompted, or configure the environment variable used in the notebook.
6. Run the chatbot tests.
7. Review the MLflow dashboard and performance comparison.
8. Run the interactive chatbot and enter `exit` to end the conversation.

**Important:** The notebook contains a troubleshooting cell referencing the original developer's local SQLite database. That cell is environment-specific and can be skipped when running the project on another computer.

The results may differ when the notebook is executed again because API response times and model behavior can vary.

## Project Scope

This is an educational experiment focused on chatbot monitoring and MLflow experiment tracking.

It is not a production chatbot deployment, and its performance results should not be interpreted as a comprehensive evaluation of model quality.

## Author

**Kevin Feracho**

Master of Science in Data Science  
Bellevue University

[GitHub Profile](https://github.com/kevinf529-cool) | [Data Science Portfolio](https://kevinf529-cool.github.io/)
