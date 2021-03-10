# Strapi Postgres

This is connected with local Postgres, you might need to check database connections before you start.


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
 - Save and publish
    
##### Update role permissions to public access
##### Install graphql plugin and paste below query to http://localhost:1337/graphql
```
query {
  apiDocumentation{
    sections{
      page{
        id
        title
        description
        sider{
          ...on ComponentSiderCode{
            id
            code
            title
            language
          }
          ...on ComponentSiderResult{
            id
            title
            result
          } 
        }
      }
    }
  }
}
```

Below is the sample response where you can see, there is no data available under `sider`.

 - No data under dynamic component `sider`
```
{
  "data": {
    "apiDocumentation": {
      "sections": [
        {
          "page": {
            "id": "1",
            "title": "Test page",
            "description": "## Test page",
            "sider": null       <-----
          }
        }
      ]
    }
  }
}
```

Once you have seen the response in graphql playground then follow the steps below: 

 - Go to `strapi-postgres/components/page/sections.json` where you will see component model like below: 
 ```
{
  "collectionName": "components_page_sections",
  "info": {
    "name": "sections",
    "icon": "align-left"
  },
  "options": {},
  "attributes": {
    "page": {
      "model": "pages"   <---- Change model to collection
    },
    "slug": {
      "type": "string"
    }
  }
}
```
 - Rename `attributes.page.model` to `attributes.page.collection`
 - Rerun the same query again, and you will be able to see data inside `sider` component, example of data below:
 ```
{
  "data": {
    "apiDocumentation": {
      "sections": [
        {
          "page": [
            {
              "id": "1",
              "title": "Test page",
              "description": "## Test page",
              "sider": [  <----- Data is now available if page attr changed to collection
                {
                  "id": "1",
                  "code": "Holla payload",
                  "title": "Request",
                  "language": "graphql"
                },
                {
                  "id": "1",
                  "title": "Result",
                  "result": "Holla response"
                }
              ]
            }
          ]
        }
      ]
    }
  }
}
```
 - By changing relation type from one-to-one to one-to-many you will be able to fetch the nested dynamic component data from graphql
 - One major thing to notice is that direct api call will not include `sider` component at all like it did in `strapi-mongo` example with broken ID type

Sample REST api response: http://localhost:1337/api-documentation

```
{
    "id": 1,
    "published_at": "2021-03-10T05:47:31.275Z",
    "created_at": "2021-03-10T05:47:26.919Z",
    "updated_at": "2021-03-10T05:50:32.684Z",
    "seo": [],
    "sections": [
        {
            "id": 1,
            "slug": "intro",
            "page": [
                {
                    "id": 1,
                    "title": "Test page",
                    "description": "## Test page",
                    "created_at": "2021-03-10T04:44:58.297Z",
                    "updated_at": "2021-03-10T04:44:58.354Z"
                }
            ]
        }
    ]
}
```


