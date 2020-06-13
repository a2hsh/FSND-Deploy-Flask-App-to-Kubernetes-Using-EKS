# Deploying a Flask API

This is the project for the fourth course in the [Udacity Full Stack Nanodegree](https://www.udacity.com/course/full-stack-web-developer-nanodegree--nd004): Server Deployment, Containerization, and Testing.

In this project, I containerized and deployed a Flask API to a Kubernetes cluster using Docker, AWS EKS, CodePipeline, and CodeBuild.

The Flask app that was used for this project consists of a simple API with three endpoints:

- `GET '/'`: This is a simple health check, which returns the response 'Healthy'. 
- `POST '/auth'`: This takes an email and password as json arguments and returns a JWT based on a custom secret.
- `GET '/contents'`: This requires a valid JWT, and returns the unencrypted contents of that token. 

## See the project in action
The project is located under the following URL:
[http://a7984eb766aea48dd88f70d97257d12a-1295984968.us-east-1.elb.amazonaws.com](http://a7984eb766aea48dd88f70d97257d12a-1295984968.us-east-1.elb.amazonaws.com)
## Testing the project
To test the project, do the following from your commandline interface:
```
export TOKEN=`curl -d '{"email":"<email>","password":"<password>"}' -H "Content-Type: application/json" -X POST http://a7984eb766aea48dd88f70d97257d12a-1295984968.us-east-1.elb.amazonaws.com/auth  | jq -r '.token'`
```
Replace the `<email>` and `<password>` with any email and password.
This will encode the data and store the token in a variable.
To decode the data, use the following command:
```
curl --request GET 'http://a7984eb766aea48dd88f70d97257d12a-1295984968.us-east-1.elb.amazonaws.com/contents' -H "Authorization: Bearer ${TOKEN}" | jq
```
You should see the email you specified in the returned json object.