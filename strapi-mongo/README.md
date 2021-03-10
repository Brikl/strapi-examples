# Strapi Mongo

This is connected with local mongoDB, you might need to check the mongo connections before you start.


### Install and run
```
$ yarn
$ yarn develop
```

### Test Steps
 - Login
 - Create a page inside `Pages` Collection types
 - Add Dynamic component `sider` with code/ result types.
 - Fill in some random values
    
### Add Page to Single type
 - Go to API documentation in Single types
 - Under `Sections`(repeatable component) add a page you have created in "Test Steps"
    
##### Go to URL http://localhost:1337/api-documentation

Below is the sample response where you can see, there is no data available under `sider`, instead there is `id` which has type Buffer,
This response also throw error in graphql plugin as the `ID` type doesn't match.

 - No data under dynamic component `sider`
 - Graphql plugin error as `ID` return Buffer instead of type `ID`
```
{
    "_id": "6048456b58544556376286f8",
    "published_at": "2021-03-10T04:06:27.236Z",
    "seo": [],
    "sections": [
        {
            "_id": "6048456b58544556376286f9",
            "slug": "intro",
            "__v": 0,
            "page": {
                "pages": [],
                "_id": "604844f848947854b13656ae",
                "description": "### Introduction",
                "slug": "introduction",
                "title": "Introduction",
                "sider": [
                    {
                        "__component": "sider.code",
                        "_bsontype": "ObjectID",
                        "id": {
                            "type": "Buffer",
                            "data": [
                                96,
                                72,
                                68,
                                248,
                                72,
                                148,
                                120,
                                84,
                                177,
                                54,
                                86,
                                175
                            ]
                        }
                    },
                    {
                        "__component": "sider.result",
                        "_bsontype": "ObjectID",
                        "id": {
                            "type": "Buffer",
                            "data": [
                                96,
                                72,
                                68,
                                248,
                                72,
                                148,
                                120,
                                84,
                                177,
                                54,
                                86,
                                176
                            ]
                        }
                    }
                ],
                "seo": [],
                "createdAt": "2021-03-10T04:03:04.918Z",
                "updatedAt": "2021-03-10T04:04:35.273Z",
                "__v": 1,
                "id": "604844f848947854b13656ae"
            },
            "id": "6048456b58544556376286f9"
        }
    ],
    "createdAt": "2021-03-10T04:04:59.674Z",
    "updatedAt": "2021-03-10T04:06:27.259Z",
    "__v": 1,
    "id": "6048456b58544556376286f8"
}
```


