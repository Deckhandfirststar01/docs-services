{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with SPLICE
{: #gettingstarted}
Last Updated: 2018-02-27

SPLICE Pre-CAT Notification Dialogs allow you to effectively communicate to your customers to best prepare them for impending catastrophic events. By providing a custom personalized response to your clients, you can ensure that the exact message you wish to purvey will be received and using SPLICE's industry leading voice will empower your customer relation experience.

By taking advantage of this API solution, you will be able to quickly and easily integrate this solution into any of your associated workflows. 
{: shortdesc}

## API Tokens
{: #Tokens}
In order to safely access the API you will need to request an API Token. To request a token, take the following steps:
- Email ccops@splicesoftware.com
    - Your email should contain the following
        - Your Name
        - Company Name
        - A short description of what you will be doing (e.g. Integration Testing, Complete Solution, etc)

Once the request has been received, a member of our team will contact you with your API Token and any additional information or contacts you may need regarding your specific use of the API.

## Customizing Solutions
{: #Solutions}
The provided solution URL through the Bluemix interface is for the purpose of integration testing and demos. SPLICE creates custom solutions to allow you to create the best possible customer interaction using customized messaging, when this stage of solution development has occurred SPLICE will provide you with a custom identifier that will be used to replace the identifier in the default URL. This will give you access to your customized solution; a unique code will be provided for each custom solution.

## API Usage
{: #Usage}
API Authentication is handled using an authorization header, which in the following examples will be denoted as **TOKEN**
The solution code will be denoted as **CODE**, please use the default of 3442 if you are still in the testing/demoing phase, otherwise use the code provided to you by SPLICE.

### Sending Data
#### Payload
The API payload is a csv file, this will be denoted as **FILE** in the examples that are to follow.
The following is an example of the structure of the file, the first row of headers is representative of the data required to use the test/demo solution. Any custom solution will have a different structure as you may wish to act on or relate different information for your custom solution.
```
First Name, Phone Number, Group
Bob, 15555555555, 1
```

#### Examples
Command Line
```
curl -X POST -H "Authorization: Token TOKEN" -F file=FILE --url "https://portal.splicesoftware.com/realtalk/api/v1/phone/CODE/"
```
{:pre}

Python
```
import requests
import unicodecsv

url = "https://api.splicesoftware.com/realtalk/api/v1/phone/{}/".format(CODE)

with open(FILE, 'rb') as call_file:
    response = requests.post(url, files={"file": call_file}, headers={"Authorization": "Token {}".format(TOKEN)})
```
{:codeblock}

#### Response
The response is the result of the processing the data sent and if successful a key that can be used to track the status of the data
```
{
"status": "success",
"code": 1002,
"data": {
    "file": "Processing campaign phone file.",
    “key”: "<key>"
    }
}
```
{:codeblock}