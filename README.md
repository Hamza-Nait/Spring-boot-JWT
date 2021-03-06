**Goals**

L&#39;The objective of the mini-project is to develop the following APIs:

1. Generation of users

method: GET

url: /api/users/generate

content-type: application/json

secured: no

parameters:

- count: number

This first REST endpoint generates a json file containing the users by respecting the following structure:

[{

  &quot;firstName&quot;: &quot;string&quot;,

 &quot;lastName&quot;: &quot;string&quot;,

 &quot;birthDate&quot;: &quot;date&quot;,

 &quot;city&quot;: &quot;ville&quot;,

 &quot;country&quot;: &quot;code iso2&quot;,

 &quot;avatar&quot;: &quot;url d&#39;une image&quot;,

 &quot;company&quot;: &quot;string&quot;,

 &quot;jobPosition&quot;: &quot;string&quot;,

 &quot;mobile&quot;: &quot;numéro de téléphone&quot;,

 &quot;username&quot;: &quot;identifiant de connexion&quot;,

 &quot;email&quot;: &quot;adresse email&quot;,

 &quot;password&quot;: &quot;mot de passe alétoire entre 6 et 10 caractères&quot;,

 &quot;role&quot;: &quot;admin ou user&quot;

}]

All the fields of this JSON file must be generated in such a way as to have plausible results using an appropriate Java library. Contents such as 'example', 'test', etc; are not acceptable.

The role field must be generated by choosing between the two values 'role' or 'admin'

By putting the URL of this API in the browser (ex: [http://localhost:9090/api/users/generate?count=100](http://localhost:9090/api/users/generate?count=100) the download of a JSON file should be triggered. The JSON should not be displayed as text in the web browser.

2. Upload of the users file and creation of users in the database

method: POST

url: /api/users/batch

content-type: multipart/form-data

secured: no

parameters:

- file: multipart-file

This second endpoint allows you to upload the JSON file generated in #1. The file must be imported into the database by checking for duplicates on the email address and the username (unique). A JSON response should be returned summarizing the total number of records, successfully imported, and not imported. Before recording in the database, the password must be encoded and not stored in clear text.

3. authentication + JWT generation

method: POST

url: /api/auth

content-type: application/json

request-body:

- username: string

- password: string

This 3rd endpoint is used to authenticate a user and generate a valid JWT token. The response is a JSON respecting the following structure:

{ &quot;accessToken&quot;: &quot;JWT token value&quot; }

The generated JWT must contain the user's email. To authenticate, it is possible to enter in the username field either the username or the email contained in the imported JSON file.

4. Viewing the profile

method: GET

url: /api/users/me

secured: yes

This 4th endpoint allows the use of the JWT token to securely access the associated user profile.

5. Viewing any profile with root privilege 

method: GET

url: /api/users/{username}

sécurisée: oui

When the JWT used corresponds to a user with the admin role, it is possible to consult the profile of any other user. A user who does not have the admin role cannot therefore access the profile of another user
