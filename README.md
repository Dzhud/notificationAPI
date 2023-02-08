# Notification API

## Overview
This API allows developers from different teams and products to target users for service notifications that can be integrated to the UX LivingLab browser extension. Developers from other products/teams can also utilize via `POST` request to target specific users. It has a single endpoint that takes `GET`, `POST`, and `PUT` http requests.

## Endpoint
http://100092.pythonanywhere.com/api/get-product/

## Items
All items have some of the following properties, with required properties in bold.

| Field        | Description |
|--------------|-------------|
| uid          |  Unique identifier associated with the notification           |
| user_id      |  User identifier field (optional but recommended)       ||
| **username**         |  Recepient of the notification. Has to be the correct value           |
| **product_id**      |  Identifier field (compulsory field)       ||
| **product_name**         |   Name of product         |
| **title**         |   Title of the notification message|
| **message** | Body of notifcation message  |
| seen         | Default value is `false`. Value changes to `true` (via `PUT` request to the endpoint) if message is viewed in the extension             |
| created_at         | Date the notification was created   |

## Example
Posting the below snippet which contain are mandatory  fields in a `POST` request
```
{
  "product_id": "99",
  "username": "Dobchinsky",  
  "product_name": "Customer Support",
  "title": "Confirm Test",
  "message": "Another test notification"
}
```
yields
```
{
    "uid": "dcb9545a-d169-40b3-9e9e-5eca8cd4b0c2",
    "user_id": null,
    "username": "Dobchinsky",
    "product_id": "99",
    "product_name": "Customer Support",
    "title": "Confirm Test",
    "message": "Another test notification",
    "seen": false,
    "created_at": "2023-02-08T19:47:14.969230Z"
  }
```

### `GET` Request
This provides all notifications to different users in the database.
```
[
  {
    "uid": "c4894d0c-fa23-47b1-b55c-aa743ac8e236",
    "user_id": null,
    "username": null,
    "product_id": "2",
    "product_name": "qwe",
    "title": "helllo",
    "message": "hy",
    "seen": false,
    "created_at": "2022-11-21T17:25:32.650553Z"
  },
  {
    "uid": "f3f058ae-7666-4f7e-b5a2-e5f4c741088b",
    "user_id": "1",
    "username": "Umair2701",
    "product_id": "2",
    "product_name": "post",
    "title": "helllo",
    "message": "trrying to post request",
    "seen": false,
    "created_at": "2022-11-25T11:16:59.444923Z"
  },
  ...]
  ```
  ### `POST` Request
  To add new notifcations. Ensure that the username is the same with the one in the DB. 
```
{
  "product_id": "19",
  "username": "Bobchinsky",  
  "product_name": "Customer Support",
  "title": "Confirm Test",
  "message": "Implement latest changes"
}
```
### `PUT` request
Only `uid` object is posted during request. This prompts `seen` object to be changed to `true` for the associated notification. This can be provisioned to distinguish 'viewed' or 'read' notifications from 'unviewed' or 'unread' notifications.   
