#Bitbucket Webhooks Plugin API Documentation
    
    This readme will document the API and how to use it.
----
    Get existing post webhooks for a specified project 

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

    OR

  * **Code:** 401 UNAUTHORIZED <br />
    **Content:** `<?xml version="1.0" encoding="UTF-8" standalone="yes"?><status><status-code>401</status-code><message>Client must be authenticated to access this resource.</message></status>`

* **Sample Call:**

    ```
    curl -u '$USER:$PASSWORD' -H "Content-Type: application/json" -X GET $BITBUCKET_SERVER_URL/rest/webhook/1.0/projects/$PROJECT/repos/$REPO/configurations
    ```

----
  Create post webhook

* **URL**

  /rest/webhook/1.0/projects/$PROJECT/repos/$REPO/configurations

* **Method:**
  
  `POST`
  
* **Data Params**

    ```javascript
    schema: {
        'title': {
            'type': 'string', 
            'description': 'The title of the post webhook - used for naming only.'
        },
        'url': {
            'type': 'string',
            'description': 'The url of the webhook.'
        },
        'enabled': {
            'type': 'boolean',
            'description': 'Toggle whether or not the webhook is enabled.'
        },
        'committersToIgnore': {
            'type': 'string',
            'description': "Comma separated list of user ids in bitbucket to ignore commits from for triggering the webhook"
        }
    }    
    ```
    
* **Success Response:**
  
  * **Code:** 201 <br />
    **Content:** 
    ```javascript
    {
        id: 21,
        title: "Jenkins hook",
        url: "http://local-jenkins.com/bitbucket-scmsource-hook/notify",
        committersToIgnore: "jdoe",
        branchesToIgnore: "",
        enabled: true
    }
    ```
* **Error Response:**

  * **Code:** 401 UNAUTHORIZED <br />
    **Content:** `<?xml version="1.0" encoding="UTF-8" standalone="yes"?><status><status-code>401</status-code><message>Client must be authenticated to access this resource.</message></status>`

  OR

  * **Code:** 400 BAD REQUEST <br />
    **Content:** 
    ```javascript
    {
        "errors": [
            {
                "context": "fake_field", 
                "exceptionName": null, 
                "message": "Unrecognized field \"fake_field\" (Class nl.topicus.bitbucket.api.WebHookConfigurationModel), not marked as ignorable\n at [Source: com.atlassian.stash.internal.web.util.web.CountingServletInputStream@527f4356; line: 3, column: 16] (through reference chain: nl.topicus.bitbucket.api.WebHookConfigurationModel[\"titlee\"])"
            }
        ]
    }
    ```

* **Sample Call:**

  curl -u user:password -H Content-Type: application/json -X POST -d {title: http://jenkins.example.com, url: http://jenkins.example.com/bitbucket-scmsource-hook/notify, enabled: true} 
    https://my.bitbucket.server.com/rest/webhook/1.0/projects/MyProject/repos/MyRepo/configurations

* **Notes:**

    This endpoint, the creation of a post webhook, can also be called as a 'PUT' request to maintain backward compatibility. However, The proper API verb for the creation of a new resource is 'POST'

----
  Update a post webhook by ID

* **URL**

  /rest/webhook/1.0/projects/$PROJECT/repos/$REPO/configurations/$WEBHOOK_ID

* **Method:**
  
  `PUT`
  
* **Data Params**

    ```javascript
    schema: {
        'title': {
            'type': 'string', 
            'description': 'The title of the post webhook - used for naming only.'
        },
        'url': {
            'type': 'string',
            'description': 'The url of the webhook.'
        },
        'enabled': {
            'type': 'boolean',
            'description': 'Toggle whether or not the webhook is enabled.'
        },
        'committersToIgnore': {
            'type': 'string',
            'description': "Comma separated list of user ids in bitbucket to ignore commits from for triggering the webhook"
        },
        'branchesToIgnore': {
            'type': 'string',
            'description': "Comma separated list of branches in the bitbucket repo to ignore commits from for triggering the webhook"
        }
    }    
    ```

* **Success Response:**
  
  * **Code:** 200 <br />
    **Content:**
    ```javascript
    {
        id: 21,
        title: "Jenkins hook",
        url: "http://local-jenkins.com/bitbucket-scmsource-hook/notify",
        committersToIgnore: "jdoe",
        branchesToIgnore: "",
        enabled: true
    }
    ```
 
* **Error Response:**

  * **Code:** 401 UNAUTHORIZED <br />
    **Content:** `<?xml version="1.0" encoding="UTF-8" standalone="yes"?><status><status-code>401</status-code><message>Client must be authenticated to access this resource.</message></status>`

  OR

  * **Code:** 400 BAD REQUEST <br />
    **Content:** 
    ```javascript
    {
        "errors": [
            {
                "context": "fake_field", 
                "exceptionName": null, 
                "message": "Unrecognized field \"fake_field\" (Class nl.topicus.bitbucket.api.WebHookConfigurationModel), not marked as ignorable\n at [Source: com.atlassian.stash.internal.web.util.web.CountingServletInputStream@527f4356; line: 3, column: 16] (through reference chain: nl.topicus.bitbucket.api.WebHookConfigurationModel[\"titlee\"])"
            }
        ]
    }
    ```

* **Sample Call:**

  curl -u user:password -H Content-Type: application/json -X PUT -d {title: http://jenkins.example.com, url: http://jenkins.example.com/bitbucket-scmsource-hook/notify, enabled: true} 
    https://my.bitbucket.server.com/rest/webhook/1.0/projects/MyProject/repos/MyRepo/configurations

* **Notes:**

    This endpoint, the update of an existing post webhook, can also be called as a 'POST' request to maintain backward compatibility. However, The proper API verb for updates to an existing resource is 'PUT'

----
  Delete a post webhook by ID

* **URL**

  /rest/webhook/1.0/projects/$PROJECT/repos/$REPO/configurations/$WEBHOOK_ID

* **Method:**
  
  `DELETE`
  
* **Success Response:**
  
  * **Code:** 204 <br />
 
* **Error Response:**

  * **Code:** 401 UNAUTHORIZED <br />
    **Content:**
    ```javascript
    {
        "errors": [
            {
                "context":null,
                "message":"Authentication failed. Please check your credentials and try again.",
                "exceptionName":"com.atlassian.bitbucket.auth.IncorrectPasswordAuthenticationException"
            }
        ]
    }
    ```

  OR

  * **Code:** 404 NOT FOUND <br />
    **Content:** 
    ```
    Webhook not found
    ```

* **Sample Call:**

  curl -u $USER:$PASSWORD -H Content-Type: application/json -X DELETE $BITBUCKET_SERVER_URL/rest/webhook/1.0/projects/$PROJECT/repos/$REPO/configurations/$WEBHOOK_ID

