# Topic 5: Loop Processing, Pagination & Rate-Limited Batching

## 1. Project Overview

This project is part of the **n8n Hands-On Level 2 Assessment**.

The goal is to create an n8n workflow that gets users from a mock API, processes them in batches, sends test emails, handles errors, and generates a final summary.

## 2. Objectives

- Get users from a mock API using pagination.
- Fetch 10 users per API request.
- Continue until all users are fetched.
- Process users in batches of 5.
- Send test emails using a mock email API.
- Handle invalid emails without stopping the workflow.
- Add a 2-second wait between batches.
- Generate a final summary.

## 3. Tools Used

- n8n
- Webhook
- HTTP Request
- Code Node (JavaScript)
- IF Node
- Edit Fields (Set)
- Loop Over Items
- Wait Node
- Mock APIs

## 4. Workflow Overview

The workflow has two parts.

**Main Workflow:**

1. Start the workflow manually.
2. Set the configuration values.
3. Fetch users from the mock API.
4. Continue fetching until all users are received.
5. Combine all users into one list.
6. Process users in batches of 5.
7. Send simulated emails.
8. Handle success and failure responses.
9. Wait 2 seconds between batches.
10. Generate the final summary.

**Mock API Workflow:**

Created two mock APIs:

- **Users API:** Returns user records based on page number.
- **Email API:** Checks email addresses and returns success or failure.

## 5. Implementation Steps

### Step 1: Create Mock APIs

Created two Webhook APIs.

**Users API:**

`GET /webhook/mock/api/users`

Returns 23 test users using pagination.

**Email API:**

`POST /webhook/mock/api/emails`

Simulates sending emails and returns success or failure.

### Step 2: Set Configuration

Configured the following values:

| Setting | Value |
|---|---|
| Page Size | 10 |
| Batch Size | 5 |
| Wait Time | 2 seconds |
| Maximum Pages | 10 |

### Step 3: Fetch Users Using Pagination

The workflow fetches users page by page.

- Page 1: 10 users
- Page 2: 10 users
- Page 3: 3 users
- Page 4: 0 users

When the API returns no users, pagination stops.

Total users fetched: **23**

### Step 4: Process Users in Batches

Used the Loop Over Items node to process users in batches of 5.

| Batch | Users |
|---|---|
| Batch 1 | 1–5 |
| Batch 2 | 6–10 |
| Batch 3 | 11–15 |
| Batch 4 | 16–20 |
| Batch 5 | 21–23 |

Total batches: **5**

### Step 5: Send Test Emails

Used the HTTP Request node to send email details to the Mock Email API.

The API checks the email address and returns a success or failure response.

No real emails are sent.

### Step 6: Handle Errors

User 13 has an invalid email address:

`bad-email-format`

The API returns an error for this user.

The workflow records the failure and continues processing the remaining users.

### Step 7: Add Wait Time

Used the Wait node to add a 2-second delay between batches.

This helps avoid sending too many API requests at once.

### Step 8: Generate Final Summary

After processing all users, the workflow generates a summary of the results.

## 6. Expected Results

| Description | Result |
|---|---|
| Total Users | 23 |
| Pages with Users | 3 |
| API Requests | 4 |
| Total Batches | 5 |
| Successful Emails | 22 |
| Failed Emails | 1 |
| Wait Between Batches | 2 seconds |

*Note: Email success and failure counts depend on collecting and combining all email API responses.*

## 7. Test Scenarios

**Test 1: Pagination**

Check that all 23 users are fetched and pagination stops when no users are returned.

**Test 2: Batch Processing**

Check that 23 users are processed in 5 batches.

**Test 3: Error Handling**

Check that User 13 fails due to an invalid email and other users continue processing.

**Test 4: Wait Time**

Check that the workflow waits 2 seconds between batches.

**Test 5: Final Summary**

Check that the final summary shows the correct results.



