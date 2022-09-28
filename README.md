# Nebula API Docs

Nebula API but doesn't seem to have a official documentation on endpoints so I decided to make this.

## User API

User API URL: https://users.api.nebula.app/api/v1

* `POST /auth/login/` - Retrieve user token

Example:

	POST /auth/login/ HTTP/1.1

	{
      "email": "email@example.com", 
      "password": "pass7word"
	}
	
	HTTP/1.1 200 OK
	
	{
      "token": "YACub2KLfe8mfmHPcUKtt6t2SMJOGPXnZbqhc3nX",
	}
	
	HTTP/1.1 400 Bad Request
	
	{
      "non_field_errors": [ "Unable to log in with provided credentials." ]
    }

You can then pass the user token in an Authorization header in subsequent user requests:

	GET /auth/user/ HTTP/1.1
	Authorization: Token YACub2KLfe8mfmHPcUKtt6t2SMJOGPXnZbqhc3nX

> Note: The token is only available until you logout

* `GET /auth/user/` - Get user details for logged in user
* `POST /auth/logout/` - Logout user
* `POST /authorization/` - Retrieve bearer token for content API

## Content API

Content API URL: https://content.api.nebula.app

* `POST https://users.api.nebula.app/api/v1/authorization` - Retrieve bearer token

Example:

	POST https://users.api.nebula.app/api/v1/authorization HTTP/1.1 Authorization: Token <user_token>
	
	HTTP/1.1 200 OK
	
	{
      "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2NjQyOTgwNzYsInN1YiI6ImM5NmIwNjRjMmEyMzRmMTc4NDBmYWYwYzM3OTUzNzYxIiwiaXNfYW5vbnltb3VzIjpmYWxzZSwiaXNfc3Vic2NyaWJlZCI6dHJ1ZSwiZW5nYWdlbWVudF9rZXkiOiJwcm9kLTExNjYzNzYiLCJlbnRpdGxlbWVudHMiOlsiYmFzaWMiXSwiYXVkIjpbImNvbnRlbnQud2F0Y2huZWJ1bGEuY29tIiwicHVzaC5hcGkubmVidWxhLmFwcCJdLCJpc3MiOiJhcGkud2F0Y2huZWJ1bGEuY29tIn0.NF4VnNd_1ZxT9-QKP3QqjyYfaXu5bbWBwHCU_TKLkEg",
	}

You can then pass the bearer in an Authorization header in subsequent content requests:

	GET /featured/ HTTP/1.1
	Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJleHAiOjE2NjQyOTgwNzYsInN1YiI6ImM5NmIwNjRjMmEyMzRmMTc4NDBmYWYwYzM3OTUzNzYxIiwiaXNfYW5vbnltb3VzIjpmYWxzZSwiaXNfc3Vic2NyaWJlZCI6dHJ1ZSwiZW5nYWdlbWVudF9rZXkiOiJwcm9kLTExNjYzNzYiLCJlbnRpdGxlbWVudHMiOlsiYmFzaWMiXSwiYXVkIjpbImNvbnRlbnQud2F0Y2huZWJ1bGEuY29tIiwicHVzaC5hcGkubmVidWxhLmFwcCJdLCJpc3MiOiJhcGkud2F0Y2huZWJ1bGEuY29tIn0.NF4VnNd_1ZxT9-QKP3QqjyYfaXu5bbWBwHCU_TKLkEg

> Note: The token is only available for 20-24 hours.

* `GET /api` - Get forum information
