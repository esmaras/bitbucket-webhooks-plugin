#Bitbucket Webhooks Plugin API Documentation
    
    This readme will document the API and how to use it.
----
    Get existing webhooks for a specified project 

* **URL**

  /rest/webhook/1.0/projects/$PROJECT/repos/$REPO/configurations

* **Method:**
  
  `GET`

* **Success Response:**
  

  * **Code:** 200 <br />
    **Content:**
    ```javascript
    [
        {
            id: 21,
            title: "Jenkins hook",
            url: "http://local-jenkins.com/bitbucket-scmsource-hook/notify",
            committersToIgnore: "jdoe",
            enabled: true
        },
        {
            id: 642,
            title: "Other Site hook",
            url: "http://local-site.com/path/to/hook",
            enabled: true
        }
    ]
    ```
 
* **Error Response:**

  * **Code:** 404 NOT FOUND <br />
    **Content:**
    ```javascript
    {
        errors: [
            {
                context: null,
                message: "Repository iprepo/eric-test3 does not exist.",
                exceptionName: "com.atlassian.bitbucket.repository.NoSuchRepositoryException"
            }
        ]
    }
    ```

* **Sample Call:**

    ```
    curl -u '$USER:$PASSWORD' -H "Content-Type: application/json" -X GET $BITBUCKET_SERVER_URL/rest/webhook/1.0/projects/$PROJECT/repos/$REPO/configurations
    ```

----
  <_Additional information about your API call. Try to use verbs that match both request type (fetching vs modifying) and plurality (one vs multiple)._>

* **URL**

  <_The URL Structure (path only, no root url)_>

* **Method:**
  
  <_The request type_>

  `GET` | `POST` | `DELETE` | `PUT`
  
*  **URL Params**

   <_If URL params exist, specify them in accordance with name mentioned in URL section. Separate into optional and required. Document data constraints._> 

   **Required:**
 
   `id=[integer]`

   **Optional:**
 
   `photo_id=[alphanumeric]`

* **Data Params**

  <_If making a post request, what should the body payload look like? URL Params rules apply here too._>

* **Success Response:**
  
  <_What should the status code be on success and is there any returned data? This is useful when people need to to know what their callbacks should expect!_>

  * **Code:** 200 <br />
    **Content:** `{ id : 12 }`
 
* **Error Response:**

  <_Most endpoints will have many ways they can fail. From unauthorized access, to wrongful parameters etc. All of those should be liste d here. It might seem repetitive, but it helps prevent assumptions from being made where they should be._>

  * **Code:** 401 UNAUTHORIZED <br />
    **Content:** `{ error : "Log in" }`

  OR

  * **Code:** 422 UNPROCESSABLE ENTRY <br />
    **Content:** `{ error : "Email Invalid" }`

* **Sample Call:**

  <_Just a sample call to your endpoint in a runnable format ($.ajax call or a curl request) - this makes life easier and more predictable._> 

* **Notes:**

  <_This is where all uncertainties, commentary, discussion etc. can go. I recommend timestamping and identifying oneself when leaving comments here._> 

