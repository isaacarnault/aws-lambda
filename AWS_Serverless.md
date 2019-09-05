## Part1: create a Lambda function

- Connect to your `AWS management console`, https://console.aws.amazon.com/<br>
- Go to Services > Lambda (Under Compute) > Create a function > Select "Author from scratch"<br>
- Function name: lambda-function-1 > Runtime: We choose Python 3.6 to write our `Lambda function`<br>
- Create a new role from AWS policy templates > Role name: lambda-execution-role<br>
- Policy templates: choose Simple microservice permissions > Create function<br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-103.png](https://i.postimg.cc/W4sbmpmb/isaac-arnault-AWS-103.png)](https://postimg.cc/NKPcBcPW)

</p>
</details>

- Go to Lambda > Functions > lambda-function-1<br>
- In <b>Function code</b> screen, double-click <b>lambda_function.py</b> and use the provided code (see lambda_function.py)<br>
- Click on File > Save and click on the top right button <b>Save</b>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-104.png](https://i.postimg.cc/ydXGmBPB/isaac-arnault-AWS-104.png)](https://postimg.cc/MMHtwCNr)

</p>
</details>

Go to <b>Basic settings</b> window and use as description: Lambda function 1 > Hit <b>Save</b><br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-aws-105.png](https://i.postimg.cc/nzc4WJxn/isaac-arnault-aws-105.png)](https://postimg.cc/cK2tKP6z)

</p>
</details>

## Part 2: deploy an API Gateway

- Click on "Add trigger" then select `API Gateway` <br>

<details>
<summary>🔴 See output</summary>
<p> 

[![isaac-arnault-AWS-106.png](https://i.postimg.cc/fk40M4Gt/isaac-arnault-AWS-106.png)](https://postimg.cc/0KfNC42P)

</p>
</details>

- API dropdown: select "Create a new API"<br>
- Security: select `AWS IAM` then click "Add"<br>

<details>
<summary>🔴 See output</summary>
<p> 

[![isaac-arnault-AWS-106.png](https://i.postimg.cc/fk40M4Gt/isaac-arnault-AWS-106.png)](https://postimg.cc/0KfNC42P)

</p>
</details>

Your <b>Designer</b> dashboard should now get updated with our new `API Gateway` as a trigger<br>

<details>
<summary>🔴 See output</summary>
<p> 

[![isaac-arnault-AWS-107.png](https://i.postimg.cc/J4JpZR4F/isaac-arnault-AWS-107.png)](https://postimg.cc/5645Mdz5)

</p>
</details>

- In <b>API Gateway</b> window click on "lambda-function-1-API"<br>

<details>
<summary>🔴 See output</summary>
<p> 

[![isaac-arnault-AWS-108.png](https://i.postimg.cc/8CWkVJ1H/isaac-arnault-AWS-108.png)](https://postimg.cc/Mc6J7GfM)

</p>
</details>

- We should now see our first `Lambda Function` Execution method<br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-110.png](https://i.postimg.cc/gjMmK3DY/isaac-arnault-AWS-110.png)](https://postimg.cc/vx6JYgkj)

</p>
</details>

- We could keep this method, but for the purpose of this gist, we're going to delete it and create a new one.<br>

- Click on "Actions" > Delete Method > "Actions" > Create Method<br>

- On <b>lambda-function-1</b> click on the dropdown and select "GET" to create a `GET request`.<br>

- Click on the check mark to save and create the `GET request`<br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-110.png](https://i.postimg.cc/gjMmK3DY/isaac-arnault-AWS-110.png)](https://postimg.cc/vx6JYgkj)

</p>
</details>

- Check "Use Lambda Proxy integration" > in Lambda Function, type: lambda-function-1 >, click "Save" <br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-112.png](https://i.postimg.cc/Bv3kXXTN/isaac-arnault-AWS-112.png)](https://postimg.cc/rDhQHyYt)

</p>
</details><br>

- When prompted by the console (Add Permission to Lambda Function), click <b>OK</b>.<br>

- Now let's go to "Actions" > Deploy API<br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-113.png](https://i.postimg.cc/J41QDZvs/isaac-arnault-AWS-113.png)](https://postimg.cc/XXz5tGVW)

</p>
</details>

- Deployment stage: use "default"<br>
- Deployment description: use "prod-deployment" then click on "Deploy"<br>
- On Stages, select default > lambda-function-1 > GET > copy Invoke URL<br>
- Go to your and create a <b>index.html</b> file. Copy paste the provided code in this gist (index.html) into your file.<br>

<details>
<summary>🔴 See output</summary>
<p> 
    
[![isaac-arnault-AWS-114.png](https://i.postimg.cc/KYJ1W3QH/isaac-arnault-AWS-114.png)](https://postimg.cc/CZnMB13G)

</p>
</details>

## Part 3: create and provision a s3 bucket

- Let's now configure `S3`. Go to Services > Storage > S3 > Create bucket: we call it "serverlessisawesome"<br>
- Select bucket > Edit public access settings > uncheck all options, click <b>Save</b> and Confirm it.

<details>
<summary>🔴 See output</summary>
<p> 
    
[![isaac-arnault-AWS-119.png](https://i.postimg.cc/3x3pbhYW/isaac-arnault-AWS-119.png)](https://postimg.cc/56k66ZHM)

</p>
</details>

- Click on <b>serverlessisawesome</b> bucket > go to Properties > Static website hosting<br>

- Select "Use this bucket to host a website" > Index document: type "index.html" > Error document: type "error.html"<br>

- Click Save<br>

- Open `Notepad` and create a <b>error.html</b> file. Copy/paste code provided in this gist (error.html)<br>

- Now we should have two files that we are going to upload to our `S3 bucket`: <b>index.html</b> and <b>error.html</b><br>

- We go back to <b>serverlessisawesome</b> bucket, click on Overview > Upload > we select both files we've created<br>

<details>
<summary>🔴 See output</summary>
<p> 
    
[![isaac-arnault-AWS-120.png](https://i.postimg.cc/SRK3G3RP/isaac-arnault-AWS-120.png)](https://postimg.cc/ygwL1fFh)

</p>
</details>

- Click on "Upload" > Select both files > Click on "Actions" > Make public<br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-121.png](https://i.postimg.cc/tgyr5wmz/isaac-arnault-AWS-121.png)](https://postimg.cc/RWsQCsm3)

</p>
</details>

To check if everything is running fine, click on <b>index.html</b> > click on <b>Object URL</b>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-122.png](https://i.postimg.cc/90vbqn7Z/isaac-arnault-AWS-122.png)](https://postimg.cc/PvQYgKK5)

</p>
</details>

On a browser page we should see our `API Gateway` in action by clicking on the button.<br>

The text is refreshing upon clicking on the button which means our trigger is working.<br>

<details>
<summary>🔴 See output</summary>
<p> 
  
[![isaac-arnault-AWS-126.png](https://i.postimg.cc/GhtmRxxd/isaac-arnault-AWS-126.png)](https://postimg.cc/ppNHY8S6)

</p>
</details>

That's all for now guys. Feel free to fork it and to spread the word about it. Thanks.
