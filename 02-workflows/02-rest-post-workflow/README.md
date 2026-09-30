 

## Lab 02 - Invoke a REST API using HTTP POST

**Workflow**

**IBM webMethods Integration \| Hands-on Workflow Lab**

------------------------------------------------------------------------

## 1. Lab Overview

In this lab, you create a webMethods Integration workflow that uses a
webhook trigger to send an HTTP POST request to the public
JSONPlaceholder REST API. You then test the HTTP action and run the
complete workflow to review the execution history.

  Item          Value
  ------------- ----------------------------------------------
  Project       `WebMethodsIntegrationLabs`
  Workflow      `REST_POST_Request`
  Trigger       Webhook
  REST API      `https://jsonplaceholder.typicode.com/posts`
  HTTP Method   POST

------------------------------------------------------------------------

## 2. What You Will Build

The completed workflow is:

``` text
Webhook → HTTP POST Request → Stop
```

When the webhook is triggered, the workflow sends a JSON payload to the
REST endpoint. The API creates a new record and returns a response
containing the submitted data, a new `id` of `101`, and a `201 Created`
status code.

------------------------------------------------------------------------

## Prerequisites

Before starting this lab, make sure you have:

-   Completed **Lab 01 -- Invoke a REST API using HTTP GET**
-   Access to **IBM webMethods Integration**
-   Access to the **Project Workspace**
-   Permission to create or edit a project and workflow
-   Internet access to the JSONPlaceholder REST API
-   The `WebMethodsIntegrationLabs` project created in Lab 01

> **Common screens:** The IBM webMethods Integration login screen,
> Project Workspace, project creation screen, and other screens that are
> unchanged from Lab 01 can be reused. There is no need to capture the
> same screenshot again unless the UI has changed.

------------------------------------------------------------------------

## 3. Create the Project

If you have already completed Lab 01, use the existing
`WebMethodsIntegrationLabs` project.

If you are setting up the lab independently:

1.  Sign in to **IBM webMethods Integration** and open webMethods
    Integration.
2.  In **Project Workspace**, select **New project**.
3.  Create the project with the name:

``` text
WebMethodsIntegrationLabs
```

4.  Open the project workspace.

The canvas provides access to **Workflows** and **Flow Services**.

**Screenshot:**\
Reuse the corresponding project creation/workspace screenshot from Lab
01.

------------------------------------------------------------------------

## 4. Create the Workflow

1.  Open **Workflows**.
2.  Select the **+** option to create a workflow.
3.  Select **Create New Workflow**.
4.  Name the workflow:

``` text
REST_POST_Request
```

5.  Add the description:

``` text
Invoke a REST API using HTTP POST and view the response
https://jsonplaceholder.typicode.com/posts
```

**Screenshot:**\
Reuse the corresponding workflow creation screenshot from Lab 01 if the
screen is unchanged.

------------------------------------------------------------------------

## 5. Configure the Webhook Trigger

1.  Select **Define Trigger**.
2.  Select **Webhook**.
3.  Configure the webhook payload with:

``` json
{
  "title": "My First Post",
  "body": "This is the post content",
  "userId": 1
}
```

4.  Select **Next**.
5.  Review the webhook options and continue.
6.  Select **Done**.

The webhook is now configured.

> **Tip:** The webhook payload contains the same fields that will be
> sent to the REST API in the HTTP POST request.

**Screenshot:**\
`images/05-webhook-trigger.png`

------------------------------------------------------------------------

## 6. Add and Configure the HTTP POST Request

1.  Add an **HTTP Request** action to the canvas.
2.  Confirm that the action is connected between the **Webhook** and
    **Stop** nodes.
3.  Open the HTTP Request configuration using the gear icon.
4.  Configure the HTTP method as **POST**.
5.  Set the URL to:

``` text
https://jsonplaceholder.typicode.com/posts
```

**Screenshot:**\
`images/06-http-post-configuration.png`

### Configure the Request Body

Change **Set Body Type** from:

``` text
x-www-form-urlencoded
```

to:

``` text
JSON
```

Enter the following JSON in the **Body** field:

``` json
{
  "title": "My First Post",
  "body": "This is the post content",
  "userId": 1
}
```

**Screenshot:**\
`images/06-http-post-configuration.png`

------------------------------------------------------------------------

## 7. Test the HTTP Request

1.  Continue to the test screen.
2.  Review the configured URL and request.
3.  Select **Test**.
4.  Open the **Output** tab.
5.  Review the response returned by JSONPlaceholder.

The response should show:

``` text
statusCode: 201
```

A `201 Created` response indicates that the POST request was successful
and a new record was created.

**Screenshot:**\
`images/07-http-post-test-output.png`

------------------------------------------------------------------------

## 8. Save and Run the Workflow

1.  Select **Done**.
2.  Save the workflow.
3.  Run the workflow from the canvas.
4.  Confirm that the workflow completes successfully.

The completed workflow should remain:

``` text
Webhook → HTTP Request → Stop
```

**Screenshot:**\
Reuse the corresponding save/run screenshot from Lab 01 if the screen is
unchanged. Otherwise:

`images/08-save-and-run.png`

------------------------------------------------------------------------

## 9. Review Execution History

1.  Select **View execution history**.
2.  Open the latest execution.
3.  Review the **Actions**, **Logs**, and **Errors** information as
    needed.
4.  Select the **HTTP Request** action and review its output.

The response should contain the submitted data and the newly created
record:

``` json
{
  "title": "My First Post",
  "body": "This is the post content",
  "userId": 1,
  "id": 101
}
```

**Screenshot:**\
`images/09-execution-details.png`

------------------------------------------------------------------------

## 10. Result

The completed workflow demonstrates the following integration pattern:

``` text
Webhook → HTTP Request (POST) → Stop
```

The HTTP request sends the JSON payload to the JSONPlaceholder endpoint
and receives a response containing the submitted data and the newly
created record ID.

The successful response includes:

-   `statusCode: 201`
-   `title: "My First Post"`
-   `body: "This is the post content"`
-   `userId: 1`
-   `id: 101`

The `id: 101` value confirms that the API created the new record.

------------------------------------------------------------------------

## 11. Key Takeaways

-   Create a project in **IBM webMethods Integration**.
-   Create and name a **Workflow**.
-   Configure a **Webhook trigger**.
-   Add an **HTTP Request** action.
-   Configure an **HTTP POST** request.
-   Set the request body type to **JSON**.
-   Send a JSON payload to a REST API.
-   Test the action and review its output.
-   Run the workflow and review **Execution History**.
-   Understand the difference between `200 OK` for a successful GET
    request and `201 Created` for a successful POST request.

------------------------------------------------------------------------

**End of Lab 02**

