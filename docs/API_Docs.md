# API Docs

Authored By: [Monal Shadi](https://github.com/Monal5031)

## Document contains information about the URL endpoints of the API, instructions over how to make request and what response to expect

:: Note :: Before testing any of the following urls make sure you have a local DB setup, server running and postman installed.

Use the given URL as Postman's target URL.

### Authentication API
1. Registration API
    
    #### Request:
    URL:
    ```
        <server_url>/api/authentication/users/registration
    ```

    Method: POST
    
    Auth type: Basic Auth
    
    Body:
    ```json
    {
      "user": {
        "email": "test_email_here",
        "username": "test_username_here",
        "password": "test_password_here",
        "other_fields...": "values"
      }
    }
    ```
    
    #### Response:
    ```json
    {
        "user": {
            "email": "test_email_here",
            "username": "test_username_here",
            "token": "unique_token_valid_for_60_days",
            "other_fields": "values"
        }
    }
    ```

2. Login API
    
    #### Request
    URL:
    ```
        <server_url>/api/authentication/users/login
    ```
    
    Method: POST
    
    Auth type: Basic Auth
    
    Body:
    ```json
    {
      "user": {
        "email": "test_email_here",
        "username": "test_username_here",
        "password": "test_password_here"
      }
    }
    ```
    or alternatively, use Bearer Token Auth and send the Token in header as in point 3.
    
    #### Response:
    ```json
    {
        "user": {
            "email": "test_email_here",
            "username": "test_username_here",
            "token": "unique_token_here_valid_for_60_days"
        }
    }
    ```

3. Update user data API.

    URL:
    ```
        <server_url>/api/authentication/users/update/
    ```
    
    #### Request
    
    -
        Method: GET
        
        Auth Type: Bearer Token
        
        Header:
        
        | Key                | Value                   |
        |:------------------:|:-----------------------:|
        | Content-Type       | application/json        |
        | Authorization      | Token token_value_here  |
    
    #### Response
    
    ```json
    {
        "user": {
            "email": "email_value",
            "username": "username_here",
            "token": "updated_token",
            "other_fields": "values_here"
        }
    }
    ```
    
    #### Request
    
    Method: POST
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |

    Body:
    
    ```json
    {
      "user": {
        "username": "username_here",
        "email": "email_here",
        "first_name": "new_first_name_here",
        "other fields": "values_here"
      }
    }
    ```
    
    #### Response
    ```json
    {
        "user": {
            "email": "email_here",
            "username": "username_here",
            "token": "updated_token",
            "first_name": "new_first_name",
            "other_fields": "values_here"
        }
    }
    ```
    

### Profile API

1. Retrieve Profile of registered user.

    #### Request
    
    URL:
    ```
        <server_url>/api/profile/retrieve/<username>/
    ```
    
    Method: GET
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    #### Response
    
    ```json
    {
        "profile": {
            "username": "username_of_requested_user",
            "following": "bool_depending_we_follow_the_user_or_not",
            "followingCount": number of people user follows,
            "followersCount": number of followers of user,
            "other_fields": "values_here"
        },
        "user": {
            "email": "email_of_user_requesting_info",
            "username": "username_of_user_requesting_info",
            "token": "updated_token_valid_for_60_days",
            "other_fields": "values_here"
        }
    }
    ```

2. Follow a registered Profile.
    
    #### Request
    
    URL:
    ```
        <server_url>/api/profile/<username_of_user_to_follow>/follow
    ```
    
    Method: POST
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    Body:
    ```json
    {
       // Nothing required but as a security backup send username and password
       "user": {
         "username": "requesting_users_username_here",
         "password": "password_here"
       } 
    }
    ```
    
    #### Response
    
    ```json
    {
        "profile": {
            "username": "username_of_user_requested",
            "bio": "bio_of_requested_user",
            "image": "img_of_requested_user",
            "following": true,
            "cover": "cover_of_requested_user"
            "followingCount": number of people user follows,
            "followersCount": number of followers of user,
        }
    }
    ```

3. Unfollow a registered Profile
    
    #### Request
    
    URL:
    ```
        <server_url>/api/profile/<username_of_user_to_follow>/follow
    ```
    
    Method: DELETE
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    Body:
    ```json
    {
       // Nothing required but as a security backup send username and password
       "user": {
         "username": "requesting_users_username_here",
         "password": "password_here"
       } 
    }
    ```
    
    #### Response
    
    ```json
    {
        "profile": {
            "username": "username_of_user_requested",
            "bio": "bio_of_requested_user",
            "image": "img_of_requested_user",
            "following": false,
            "cover": "cover_of_requested_user"
            "followingCount": number of people user follows,
            "followersCount": number of followers of user,
        }
    }
    ```

4. Retrieve all profiles user is following

    #### Request
    
    URL:
    ```
        <server_url>/api/profile/following/?user=A&limit=N&offset=M
    ```
    N = Limit the number of profile to fetch
    
    M = offset of the profiles to send
    
    A = username of profile whose following to retrieve
    
    Method: GET
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    Body:
    ```json
    {
       // Nothing required but as a security backup send username and password
       "user": {
         "username": "requesting_users_username_here",
         "password": "password_here"
       } 
    }
    ```
    
    #### Response
    
    ```json
    {
        "profiles": [
           {
             // First profile
           },
           {
             // Second profile
           }
        ] 
    }
    ```

5. Retrieve all profiles of followers of user

    #### Request
    
    URL:
    ```
        <server_url>/api/profile/followers/?user=A&limit=N&offset=M
    ```
    N = Limit the number of profile to fetch
    
    M = offset of the profiles to send
    
    A = username of profile whose followers to retrieve
    
    Method: GET
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    Body:
    ```json
    {
       // Nothing required but as a security backup send username and password
       "user": {
         "username": "requesting_users_username_here",
         "password": "password_here"
       } 
    }
    ```
    
    #### Response
    
    ```json
    {
        "profiles": [
           {
             // First profile
           },
           {
             // Second profile
           }
        ] 
    }
    ```

### Post API

1. Create a new POST

    #### Request
    
    URL:
    ```
        <server_url>/api/post/create
    ```
    
    Method: POST
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    Body:
    ```json
    {
        "post": {
            "description": "Post description",
            "body": "Post body",
            "title": "Post Title",
            "tagList": ["tag1", "tag2"]
        }
    }
    ```
    
    #### Response
    
    ```json
    {
        "post": {
            "author": {
                "username": "username_of_user_creating_post",
                "bio": "bio_of_same_user",
                "image": "img_of_same_user",
                "following": false,
                "cover": "cover_of_same_user"
            },
            "body": "body of created post",
            "createdAt": "Timestamp of post created time, like: 2018-11-07T11:19:36.288463+00:00",
            "description": "description of created post",
            "favorited": false,
            "favoritesCount": 0,
            "slug": "unique slug of post",
            "tagList": [
                "tag1",
                "tag2"
            ],
            "title": "title of created post",
            "updatedAt": "Timestamp of post last updated time, like 2018-11-07T11:19:36.288520+00:00"
        }
    }
    ```

2. Retrieve all posts by author

    #### Request
    
    URL:
    ```
        <server_url>/api/post/view/?limit=N&offset=M&author=A
        
    ```
    N = number of posts to fetch.
    
    M = number of posts to send from fetched.
    
    A = username of author whose post to fetch
    
    Method: GET
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    #### Response
    
    ```json
    {
        "posts": [
           {
             // First post
           },
           {
             // Second post
           }
        ] 
    }
    ```

3. Retrieve a single post

    #### Request
    
    URL:
    ```
        <server_url>/api/post/view/<post_slug>
        
    ```
    
    Method: GET
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    #### Response
    
    ```json
    {
        "post": {
            "author": {
                "username": "username_of_author",
                "bio": "",
                "image": "img of author",
                "following": "bool depending whether we follow or not",
                "cover": "cover of author"
            },
            "body": "body of post",
            "createdAt": "timestamp of post create, like: 2018-11-03T10:13:26.081688+00:00",
            "description": "description of post",
            "favorited": "bool depending if we have favorited the post",
            "favoritesCount": "int: number of favorites of post",
            "slug": "post slug",
            "tagList": ["tag1", "tag2"],
            "title": "title of post",
            "updatedAt": "timestamp of post update, like: 2018-11-06T14:58:15.468138+00:00"
        }
    }
    ```

4. Update content of the post

    #### Request
    
    URL:
    ```
        <server_url>/api/post/update/<post_slug>
        
    ```
    
    Method: POST
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    Body
    
    ```json
    {
        "post": {
            "field_to_update": "updated_value"
        }
    }
    ```
    
    #### Response
    
    ```json
    {
        "post": {
            "author": {
                "username": "username_of_author",
                "bio": "",
                "image": "img of author",
                "following": "bool depending whether we follow or not",
                "cover": "cover of author"
            },
            "body": "body of post",
            "createdAt": "timestamp of post create, like: 2018-11-03T10:13:26.081688+00:00",
            "description": "description of post",
            "favorited": "bool depending if we have favorited the post",
            "favoritesCount": "int: number of favorites of post",
            "slug": "post slug",
            "tagList": ["tag1", "tag2"],
            "title": "title of post",
            "updatedAt": "timestamp of post update, like: 2018-11-06T14:58:15.468138+00:00"
        }
    }
    ```

5. Retrieve all posts by following of users

    #### Request
    
    URL:
    ```
        <server_url>/api/post/feed/?limit=N&offset=M
        
    ```
    N = number of posts to fetch.
    
    M = number of posts to send from fetched.
    
    Method: GET
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    #### Response
    
    ```json
    {
        "posts": [
           {
             // First post
           },
           {
             // Second post
           }
        ] 
    }
    ```

6. Delete a post
    
    #### Request
    
    URL:
    ```
        <server_url>/api/post/<post_slug>/delete/
        
    ```
    
    Method: GET
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    #### Response
    
    No response body, just a `204 NO_CONTENT` status.

7. Add or remove post from favorite.

    #### Request
    
    URL:
    ```
        <server_url>/api/post/<post_slug>/favorite/
        
    ```
    
    Method: GET
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    #### Response
    
    ```json
    {
        "post": {
            "author": {
                // author data
            },
         "favorited": true
         // post data
        }
    }
    ```
    
    Method: DELETE
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    #### Response
    
    ```json
    {
        "post": {
            "author": {
                // author data
            },
        "favorited": false,
        "favoritesCount": int count
        // post data
        }
    }
    ```

8. Adding and removing an upvote on post

    #### Request
    
    URL:
    ```
        <server_url>/api/post/<post_slug>/upvote/
        
    ```
    
    Method: GET
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    #### Response
    
    ```json
    {
        "post": {
            "author": {
                // author data
            },
         "upvoted": true,
         "upvotesCount": int count
         // post data
        }
    }
    ```
    
    Method: DELETE
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    #### Response
    
    ```json
    {
        "post": {
            "author": {
                // author data
            },
        "upvoted": false,
        "upvotesCount": int count
        // post data
        }
    }
    ```

9. Adding and removing an downvote on post

    #### Request
    
    URL:
    ```
        <server_url>/api/post/<post_slug>/downvote/
        
    ```
    
    Method: GET
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    #### Response
    
    ```json
    {
        "post": {
            "author": {
                // author data
            },
         "downvote": true,
         "downvotesCount": int count
         // post data
        }
    }
    ```
    
    Method: DELETE
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    #### Response
    
    ```json
    {
        "post": {
            "author": {
                // author data
            },
        "downvoted": false,
        "downvotesCount": int count
        // post data
        }
    }
    ```


### Page API

1. Retrieve page suggestions whom user is not following.

    #### Request
    
    URL:
    ```
        <server_url>/api/profile/discover/pages
        
    ```
    
    Method: GET
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    #### Response
    
    ```json
    {
        "profiles": [
           {
             // First profile
           },
           {
             // Second profile
           }
        ] 
    }
    ```

### Comment API

1. Create a comment
    
    #### Request
    
    URL:
    ```
        <server_url>/api/post/<post_slug>/comments/create/
    ```
    
    Method: POST
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    Body
    ```json
    {
       "comment": {
           "body": "body of cmment"
       }
    }
    ```
    
    #### Response
    
    ```json
    {
        "comment": {
            "id": int id of comment,
            "author": {
                // author data
            },
            "body": "body of comment",
            "createdAt": "timestamp",
            "updatedAt": "timestamp",
            "post_slug": "slug of post"
        }
    }
    ```

2. View all comments of a post.
    
    #### Request
    
    URL:
    ```
        <server_url>/api/post/<post_slug>/comments/view?limit=N&offset=M
    ```
    
    N = number of comments to fetch.
    
    M = number of comments to send from fetched.
    
    Method: GET
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    #### Response
    
    ```json
    {
        "comments": [
            // first comment,
            // second comment
        ]
    }
    ```

3. View a single comment

    #### Request
    
    URL:
    ```
        <server_url>/api/post/<post_slug>/comments/view/<commnt_pk>/
    ```
    
    Method: GET
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    #### Response
    
    ```json
    {
        "comment": {
            "id": int id of comment,
            "author": {
                // author data
            },
            "body": "body of comment",
            "createdAt": "timestamp",
            "updatedAt": "timestamp",
            "post_slug": "slug of post"
        }
    }
    ```

4. Update a comment

    #### Request
    
    URL:
    ```
        <server_url>/api/post/<post_slug>/comments/update/<comment_pk>
        
    ```
    
    Method: POST
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    Body
    
    ```json
    {
        "comment": {
            "field_to_update": "updated_value"
        }
    }
    ```
    
    #### Response
    
    ```json
    {
        "comment": {
            "author": {
                // author data
            },
            // comment data
        }
    }
    ```

5. Delete a comment
    
    #### Request
    
    URL:
    ```
        <server_url>/api/post/<post_slug>/comments/delete/<comment_pk>/
        
    ```
    
    Method: GET
    
    Auth Type: Bearer Token
    
    Header:
    
    | Key                | Value                   |
    |:------------------:|:-----------------------:|
    | Content-Type       | application/json        |
    | Authorization      | Token token_value_here  |
    
    #### Response
    
    No response body, just a `204 NO_CONTENT` status.
