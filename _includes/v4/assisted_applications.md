## Assisted Application

### Initialize an Assisted Application

In order to be able to initialize an assisted application, you must have the
[assisted-journey]({{ site.baseurl }}/features/#assisted-journey) feature enabled.

```
POST {{ site.data.globals.api_prefix }}/initialize-assisted-application
```

#### Parameters

Name | Required | Type | Description
--- | --- | --- | ---
`$.email` | Yes | string | The consumers Email Address.
`$.*` | Yes | object | Required fields as described in the [Initialize an Application]({{ site.baseurl }}/api/#initialize-an-application) section.

#### Example with Required Fields

```json
{
    "email": "fillibert.labingi@gmail.com",
    "installation": "NoveltyRock",
    "order": {
        "reference": "NRE01234",
        "amount": 49995,
        "description": "Novelty Rock",
        "validity": "2015-12-25T12:00:00+00:00"
    },
    "products": {
        "group": "FF",
        "options": [
            "*"
        ]
    }
}
```

#### Response
Name | Required | Type | Description
--- | --- | --- | ---
`$.application` | Yes | long | As described in the [Initialize an Application]({{ site.baseurl }}/api/#initialize-an-application) section.
`$.url` | Yes | string | As described in the [Initialize an Application]({{ site.baseurl }}/api/#initialize-an-application) section.
`$.user` | no | Integer / null | User ID when user exists, null otherwise.
`$.profile` | no | [profile]({{ site.baseurl }}/api/#profile) | Profile Information.

#### Different types of responses

##### Account Already Exists
```json
{
    "application": 123,
    "url": "https://checkout.paybreak.com/?id=123&token=ab2141f3b25",
    "user": 12345
}
```

##### No account exists
```json
{
    "application": 123,
    "url": "https://checkout.paybreak.com/?id=123&token=ab2141f3b25",
    "user": null,
    "profile": {
        "create": "{{ site.data.globals.api_prefix }}/applications/123/users"
    }
}
```

##### Cannot Provide Finance
```json
{
    "code": 400,
    "message": "We cannot provide finance based on the information provided"
}
```

### Create Profile

```
POST {{ site.data.globals.api_prefix }}/initialize-assisted-application
```
#### Parameters

Name                     | Required | Type    | Description
-------------------------|----------|---------|------------
`$.title`                | Yes      | string  |
`$.first_name`           | Yes      | string  |
`$.last_name`            | Yes      | string  |
`$.date_of_birth`        | Yes      | string  |
`$.phone_home`           | No       | string  |
`$.phone_mobile`         | No       | string  |
`$.number_of_dependants` | No       | integer |
`$.marital_status`       | No       | string  |

#### Response
```json
{
    "user": 456,
    "profile": {
        "address": "{{ site.data.globals.api_prefix }}/users/456/address",
        "employment": "{{ site.data.globals.api_prefix }}/users/456/employment",
        "financial": "{{ site.data.globals.api_prefix }}/users/456/financial"
    }
}
```

### Add Address

### Add Employment Details

### Add Financial Details

### Dictionary Marital Status

```
GET {{ site.data.globals.api_prefix }}/dictionaries/marital-status
```

#### Response
```json
[
    {
        "id": 1,
        "description": "Cohabiting, but not married"
    }
]
```