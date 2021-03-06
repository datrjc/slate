<% t_scope('cashflow_md') { %>
# <%=t('.header')%>

<% t_scope('categories_and_categorygroups') { %>
## <%=t('.header')%>

- URL: `/pl/categories`
- <%=t('method')%>: `POST`
- <%=t('.request_data_format')%>: `JSON`

<%=t('.desc1')%>
<aside class="well">[
    <%=t('category_group')%> 1
        |__ <%=t('category')%> 1      <- <%=t('.default_category_of_group')%>
        |__ <%=t('category')%> 2
        |__ ...
    <%=t('category_group')%> 2
        |__ <%=t('category')%> 3      <- <%=t('.default_category_of_group')%>
        |__ ...
    ...
]</aside>

<%=t('.desc2')%>

***<%=t('request')%>***

<% t_scope('.request.categorygroups_s_parameters', use_html_br: true) { %>
<%=t('.header')%>

| <%=t('parameter')%> | <%=t('name')%> | <%=t('remarks')%> | <%=t('required')%> | <%=t('data_form')%> |
|---------------------|----------------|-------------------|--------------------|---------------------|
| id | <%=t('.fields.id')%> | | ○ | string |
| type | <%=t('.fields.type')%> | <%=t('.fields.type_desc')%> | ○ | integer |
| name | <%=t('.fields.name')%> | <%=t('multilingual_support')%> | ○ | string |
<% } %>

<% t_scope('.request.categories_s_parameters', use_html_br: true) { %>

<%=t('.header')%>

| <%=t('parameter')%> | <%=t('name')%> | <%=t('remarks')%> | <%=t('required')%> | <%=t('data_form')%> |
|---------------------|----------------|-------------------|--------------------|---------------------|
| id | <%=t('.fields.id')%> | <%=t('.fields.id_desc')%>　| ○ | string |
| name | <%=t('.fields.name')%> | <%=t('multilingual_support')%> | ○ | string |
<% } %>

> <%=t('request')%>

```shell
curl -v -X POST <%= BASE_PATH %>/pl/categories \
     --data '
     [
       {
         "id": "1",
         "type": 1,
         "name": {
           "ja": "賃料",
           "en": "Rent"
         },
         "categories": [
           {
             "id": "1",
             "name": {
               "ja": "賃料",
               "en": "Rent"
             }
           },
           {
             "id": "2",
             "name": {
               "ja": "管理費",
               "en": "Management fee"
             }
           }
         ]
       },
       {
         "id": "2",
         "type": 0,
         "name": {
           "ja": "仲介費",
           "en": "Real Estate Agent fee"
         },
         "categories": [
           {
             "id": "3",
             "name": {
               "ja": "仲介費",
               "en": "Real Estate Agent fee"
             }
           }
         ]
       }
     ]
     ' \
     <%= HEADER_ACCESS_TOKEN %>
```

> <%=t('response')%>

```json
{
    "err": 0
}
```
<% } %>

<% t_scope('property_cashflow.upsert') { %>
## <%=t('.header')%>

<%=t('.desc')%>

- URL: `/pl/:gl_id/properties/:property_id`
- <%=t('method')%>: `POST`

***<%=t('request')%>***

<% t_scope('.fields', use_html_br: true) { %>
| <%=t('parameter')%> | <%=t('name')%> | <%=t('remarks')%> | <%=t('required')%> | <%=t('data_form')%> |
|---------------------|----------------|-------------------|--------------------|---------------------|
| gl_id | <%=t('.gl_id')%> | <%=t('.gl_id_desc')%> | ○ | string |
| property_id | <%=t('.property_id')%> | | ○ | string |
| category_id | <%=t('.category_id')%> | | △ | string |
| month | <%=t('.month')%> | <%=t('format_yyyymm')%> | × | string |
| payment_date | <%=t('.payment_date')%> | <%=t('format_yyyymmdd')%> | × | string |
| amount | <%=t('.amount')%> | <%=t('unit_yen')%> | △ | double |
| transaction_id | <%=t('.transaction_id')%> | <%=t('.transaction_id_desc')%> | × | string |
| remarks | <%=t('.remarks')%> | | × | string |
| payee_id | <%=t('payee_id')%> | | × | string |
| payee_name | <%=t('payee_name')%> | | × | string |
| payer_id | <%=t('payer_id')%> | | × | string |
| payer_name | <%=t('payer_name')%> | | × | string |
| published | <%=t('.published')%> | <%=t('.published_desc')%> | ○ | bool |
<% } %>

```shell
curl -v -X POST <%= BASE_PATH %>/pl/1/properties/1 \
     --data '
     {
       "category_id": "2",
       "month": "2018-06",
       "payment_date": "2018-05-25",
       "amount": 200000,
       "transaction_id": "00012345",
       "remarks": "５月分の賃料",
       "payee_id": "o1",
       "payee_name": "山田太郎",
       "payer_id": "t1",
       "payer_name": "佐藤太郎",
       "published": true
     }
     ' \
     <%= HEADER_ACCESS_TOKEN %>
```
<% } %>

<% t_scope('property_cashflow.delete') { %>
## <%=t('.header')%>

<%=t('.desc')%>

- URL: `/pl/:gl_id/properties/:property_id`
- <%=t('method')%>: `DELETE`

```shell
curl -v -X DELETE <%= BASE_PATH %>/pl/1/properties/1 \
     <%= HEADER_ACCESS_TOKEN %>
```
<% } %>

<% t_scope('room_cashflow.upsert') { %>
## <%=t('.header')%>

<%=t('.desc')%>

- URL: `/pl/:gl_id/rooms/:room_id`
- <%=t('method')%>: `POST`

***<%=t('request')%>***

<% t_scope('.fields', use_html_br: true) { %>
| <%=t('parameter')%> | <%=t('name')%> | <%=t('remarks')%> | <%=t('required')%> | <%=t('data_form')%> |
|---------------------|----------------|-------------------|--------------------|---------------------|
| gl_id | <%=t('.gl_id')%> | <%=t('.gl_id_desc')%> | ○ | string |
| room_id | <%=t('.room_id')%> | | ○ | string |
| category_id | <%=t('.category_id')%> | | △ | string |
| month | <%=t('.month')%> | <%=t('format_yyyymm')%> | × | string |
| payment_date | <%=t('.payment_date')%> | <%=t('format_yyyymmdd')%> | × | string |
| amount | <%=t('.amount')%> | <%=t('unit_yen')%> | △ | double |
| transaction_id | <%=t('.transaction_id')%> | <%=t('.transaction_id_desc')%> | × | string |
| remarks | <%=t('.remarks')%> | | × | string |
| payee_id | <%=t('payee_id')%> | | × | string |
| payee_name | <%=t('payee_name')%> | | × | string |
| payer_id | <%=t('payer_id')%> | | × | string |
| payer_name | <%=t('payer_name')%> | | × | string |
| published | <%=t('.published')%> | <%=t('.published_desc')%> | ○ | bool |
<% } %>

```shell
curl -v -X POST <%= BASE_PATH %>/pl/1/rooms/1 \
     --data '
     {
       "category_id": "2",
       "month": "2018-06",
       "payment_date": "2018-05-25",
       "amount": 200000,
       "transaction_id": "00012345",
       "remarks": "５月分の賃料",
       "payee_id": "o1",
       "payee_name": "山田太郎",
       "payer_id": "t1",
       "payer_name": "佐藤太郎",
       "published": true
     }
     ' \
     <%= HEADER_ACCESS_TOKEN %>
```
<% } %>

<% t_scope('room_cashflow.delete') { %>
## <%=t('.header')%>

<%=t('.desc')%>

- URL: `/pl/:gl_id/rooms/:room_id`
- <%=t('method')%>: `DELETE`

```shell
curl -v -X DELETE <%= BASE_PATH %>/pl/1/rooms/1 \
     <%= HEADER_ACCESS_TOKEN %>
```
<% } %>

<% } %>