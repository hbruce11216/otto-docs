Table of Contents
- [APIs](#apis)
  - [Stages](#stages)
    - [Dev](#dev)
      - [Base URL](#base-url)
    - [Staging](#staging)
      - [Base URL](#base-url-1)
  - [Authorization](#authorization)
    - [Token Endpoint](#token-endpoint)
- [Persona](#persona)
  - [Get Persona](#get-persona)
    - [Request](#request)
    - [Response](#response)
- [Email Templates](#email-templates)
  - [Get Email Templates](#get-email-templates)
    - [Request](#request-1)
    - [Response](#response-1)
  - [Create Custom Template](#create-custom-template)
    - [Request](#request-2)
    - [Payload](#payload)
    - [Response](#response-2)
  - [Update Custom Template](#update-custom-template)
    - [Request](#request-3)
    - [Payload](#payload-1)
    - [Response](#response-3)
  - [Delete Custom Template](#delete-custom-template)
    - [Request](#request-4)
  - [Response](#response-4)
  - [Get Email Template Placeholders](#get-email-template-placeholders)
    - [Request](#request-5)
    - [Response](#response-5)
- [Input](#input)
  - [Request](#request-6)
  - [Payload](#payload-2)
  - [Response](#response-6)
- [Profiles](#profiles)
  - [Request](#request-7)
  - [Response](#response-7)

# APIs
This documentation contains the list of APIs currently exposed in our platform through Amazon API Gateway.

## Stages
We currently have two API Stages, Dev and Staging.

### Dev
#### Base URL
https://52x900y0cf.execute-api.us-east-1.amazonaws.com/dev

### Staging
#### Base URL
https://mj3cr70mfi.execute-api.us-east-1.amazonaws.com/staging

## Authorization
Authorization is done using OAuth 2.

### Token Endpoint
* **Dev** - 	
https://dev-sellwithotto-ai.auth.us-east-1.amazoncognito.com/oauth2/token
* **Staging** - https://staging-sellwithotto-ai.auth.us-east-1.amazoncognito.com/oauth2/token


# Persona
The persona API provides the list of persona roles/industries currently supported.

## Get Persona
### Request
`GET ${baseURL}/persona`
### Response
```json
{
   "data":{
      "industries":[
         
      ],
      "roles":[
         {
            "id":"ROLE_FINANCE",
            "value":"Finance"
         },
         {
            "id":"ROLE_HEALTHCARE_SERVICES",
            "value":"Healthcare Services"
         },
         {
            "id":"ROLE_HUMAN_RESOURCES",
            "value":"Human Resources"
         },
         {
            "id":"ROLE_INFORMATION_TECHNOLOGY",
            "value":"Information Technology"
         },
         {
            "id":"ROLE_MARKETING",
            "value":"Marketing"
         },
         {
            "id":"ROLE_OPERATIONS",
            "value":"Operations"
         },
         {
            "id":"ROLE_SALES",
            "value":"Sales"
         },
         {
            "id":"ROLE_SUPPORT",
            "value":"Support"
         }
      ]
   }
}
```

# Email Templates
Email templates API provides list of system default and user custom email templates.

## Get Email Templates
### Request
`GET ${baseURL}/email-templates`

### Response
```json
{
   "data":[
      {
         "pk":"EML_e883c633-43e2-4358-b796-e032c0d67942",
         "sk":"EML_e883c633-43e2-4358-b796-e032c0d67942",
         "value":"<p>Hey {{first_name}},</p><br /><p>I noticed that you're focused on {{keyword}} and {{keyword}} and wanted to shoot you a quick note.</p><br /><p>Given your role at {{company}}, it would be great to get 30 minutes on your calendar to show you how the technology can benefit you.</p><br /><p>When do you have time to connect?</p>"
      },
      {
         "pk":"USR_40f15296-e4d2-4e6a-841d-016b06c00189",
         "sk":"EML_dcb99a1b-4bee-4c88-b77d-4fcdb0f68748",
         "value":"<p>Hi {{first_name}},</p><p><br></p><p>I got to know you through the article \"{{article}}\" at {{publication}}, so I quickly searched for your profile on LinkedIn. Noticed that you're focused on {{keyword}} and {{keyword}} so I wanted to shoot you a quick note.</p><p><br></p><p>Given your role at {{company}}, it would be great to get 30 minutes on your calendar to show you how the technology can benefit you.</p><p><br></p><p>When do you have time to connect?</p>"
      }
   ]
}
```

## Create Custom Template
### Request
`POST ${baseURL}/email-templates`

### Payload
```json
{
    "emailTemplate": "...."
}
```

### Response
```json
{
    "data": {
         "pk": "...",
         "sk": "...",
         "value": "..."
    }
}
```

## Update Custom Template
### Request
`PUT ${baseURL}/email-templates/{sk}`

**{sk}** - The sort/range key of the email template to update

### Payload
```json
{
    "emailTemplate": "...."
}
```

### Response
```json
{
    "data": {
         "pk": "...",
         "sk": "...",
         "value": "..."
    }
}
```

## Delete Custom Template
### Request
`DELETE ${baseURL}/email-templates/{sk}`

**{sk}** - The sort/range key of the email template to update

## Response
```json
{
    "data": "Success"
}
```

## Get Email Template Placeholders
Returns the list of placeholders that can be used when creating / updating an email template.

### Request
`GET ${baseURL}/email-templates/placeholders`

### Response
```json
{
   "data":[
      "first_name",
      "company",
      "keyword",
      "article",
      "publication",
      "article_description"
   ]
}
```

# Input
The input API endpoint is the main submission endpoint for processing user submitted email generation parameters.

## Request
`POST ${baseURL}/input`

## Payload
```json
{
   "linkedInProfiles":[
      "https://www.linkedin.com/in/arjaynacion/"
   ],
   "roleId":"ROLE_INFORMATION_TECHNOLOGY",
   "emailTemplateId":"EML_e883c633-43e2-4358-b796-e032c0d67942|EML_e883c633-43e2-4358-b796-e032c0d67942"
}
```

## Response
```json
{
   "data":{
      "requestId":"7b043f7a-c651-486b-99ae-589d52f405ab",
      "batchProcessing":false,
      "profiles":[
         {
            "url":"https://www.linkedin.com/in/arjaynacion",
            "name":"Arjay Nacion",
            "jobTitle":"Senior Manager - Full Stack Dev Lead",
            "company":"RCG Global Services Full-time",
            "imageUrl":"https://media-exp1.licdn.com/dms/image/C5603AQHVv80_WECYOQ/profile-displayphoto-shrink_200_200/0/1517688659415?e=1642636800&v=beta&t=R23o7B3Jxkqj6smCWXHIX7qZuTaYhkYc11kMozR58hQ",
            "emailBody":"<p>Hey Arjay,</p><br /><p>I noticed that you're focused on migrations and integrations and digital and wanted to shoot you a quick note.</p><br /><p>Given your role at RCG Global Services, it would be great to get 30 minutes on your calendar to show you how the technology can benefit you.</p><br /><p>When do you have time to connect?</p>",
            "matchedKeywords":[
               "migrations and integrations",
               "digital",
               "cloud modernization",
               "IT",
               "infrastructure",
               "continuous improvement",
               "business",
               "companies"
            ]
         }
      ]
   }
}
```

# Profiles
The profiles endpoint provides the scraped data for a given LinkedIn Profile URL.

## Request
`GET ${baseURL}/profiles?uri={linkedInProfileUri}`

**{linkedInProfileUri}** - The LinkedIn Profile URL (e.g. https://www.linkedin.com/in/johndoe/)

## Response
```json
{
    "data": {
        "scraped": "2021-11-20T05:48:30.080Z",
        "expiry": "2021-11-21T05:48:30.080Z",
        "uri": "https://www.linkedin.com/in/arjaynacion",
        "profile": {
            "profile": {
                "name": "Arjay Nacion",
                "headline": "Senior Manager - Full Stack Dev Lead at RCG Global Services",
                "location": "Metro Manila, National Capital Region, Philippines",
                "summary": "• Java, Spring, Spring Boot, SpringData, MongoDB, PostgreSQL, Oracle, AWS, Docker, REST, AngularJS, Angular, ReactJS\n• Results-driven software craftsman with ...",
                "imageurl": "https://media-exp1.licdn.com/dms/image/C5603AQHVv80_WECYOQ/profile-displayphoto-shrink_200_200/0/1517688659415?e=1642636800&v=beta&t=R23o7B3Jxkqj6smCWXHIX7qZuTaYhkYc11kMozR58hQ"
            },
            "positions": [
                {
                    "title": "Senior Manager - Full Stack Dev Lead",
                    "description": null,
                    "companyName": "RCG Global Services Full-time",
                    "location": "Makati",
                    "date1": "Feb 2019 – Present",
                    "date2": "2 yrs 10 mos",
                    "roles": []
                },
                {
                    "title": "SSE III",
                    "description": null,
                    "companyName": "Fuji Xerox Document Management Solutions Full-time",
                    "location": "Taguig",
                    "date1": "Jul 2017 – Apr 2018",
                    "date2": "10 mos",
                    "roles": []
                },
                {
                    "title": "BrokerHub",
                    "description": "Driving innovations in the development team's technologies and methodologies.\n* Spearheaded the migration of SVN repositories to Git and introduced Gitflow Workflow\n* ...",
                    "companyName": null,
                    "location": "Eastwood, Quezon City",
                    "date1": "Jun 2016 – Jun 2017",
                    "date2": "1 yr 1 mo",
                    "roles": [
                        {
                            "title": "Chief Technology Officer",
                            "description": null
                        },
                        {
                            "title": "Software Architect",
                            "description": "Driving innovations in the development team's technologies and methodologies...."
                        }
                    ]
                },
                {
                    "title": "Senior Java Developer",
                    "description": "FXDMS Philippines Inc (formerly Salmat Services Inc.). Continued serving the role of Senior Java Developer.",
                    "companyName": "Fuji Xerox Document Management Solutions Full-time",
                    "location": "Mckinley Hill, Taguig",
                    "date1": "Sep 2012 – Jan 2015",
                    "date2": "2 yrs 5 mos",
                    "roles": []
                },
                {
                    "title": "Freelance Developer",
                    "description": null,
                    "companyName": "Mind Alliance Freelance",
                    "location": null,
                    "date1": "2013",
                    "date2": "less than a year",
                    "roles": []
                },
                {
                    "title": "Senior Java Developer",
                    "description": "Worked as Senior Java Developer primarily on projects using GWT, Spring, Hibernate and XML Web Services.\n\nBeen deployed to Sydney, Australia twice to do project work and is currently working as one of the key developers for a new project creating the Persistence and WebService APIs.\n\nConducts technical interviews with Java applicants.\nsee less",
                    "companyName": "Salmat Full-time",
                    "location": "Philippines",
                    "date1": "Jun 2012 – Sep 2012",
                    "date2": "4 mos",
                    "roles": []
                },
                {
                    "title": "Java Developer",
                    "description": null,
                    "companyName": "Ideyatech, Inc. Full-time",
                    "location": "Pasig City",
                    "date1": "May 2010 – Jun 2012",
                    "date2": "2 yrs 2 mos",
                    "roles": []
                }
            ],
            "skills": [
                {
                    "title": "Hibernate"
                },
                {
                    "title": "Web Services"
                },
                {
                    "title": "MySQL"
                },
                {
                    "title": "Software Development"
                },
                {
                    "title": "Agile Methodologies"
                },
                {
                    "title": "Web Development"
                },
                {
                    "title": "OOP"
                },
                {
                    "title": "Object Oriented Design"
                },
                {
                    "title": "Web Applications"
                },
                {
                    "title": "Unit Testing"
                },
                {
                    "title": "Integration"
                },
                {
                    "title": "Mobile Applications"
                },
                {
                    "title": "Scrum"
                },
                {
                    "title": "Java web applications"
                },
                {
                    "title": "Front-end Development"
                },
                {
                    "title": "Maven"
                },
                {
                    "title": "Java"
                },
                {
                    "title": "Spring"
                },
                {
                    "title": "JavaScript"
                }
            ],
            "educations": [
                {
                    "title": "Mabini Colleges - Daet, Camarines Norte",
                    "degree": "BS",
                    "url": "https://www.linkedin.com/search/results/all/?keywords=Mabini%20Colleges%20-%20Daet%2C%20Camarines%20Norte",
                    "fieldOfStudy": "Computer Science",
                    "date1": "2006",
                    "date2": "2010"
                },
                {
                    "title": "Mabini Colleges - Daet, Camarines Norte",
                    "degree": "Associate's Degree",
                    "url": "https://www.linkedin.com/search/results/all/?keywords=Mabini%20Colleges%20-%20Daet%2C%20Camarines%20Norte",
                    "fieldOfStudy": "Computer System Programming",
                    "date1": "2004",
                    "date2": "2006"
                }
            ]
        }
    }
}
```