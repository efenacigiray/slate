---
title: Storyly API Reference

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

search: true
code_clipboard: true
---

# Getting Started

Welcome to the Storyly API! You can use Storyly API to manage your story groups and stories via HTTP requests.

To use the external API, you will need to create a unique API Token from dashboard.

Login to dashboard, navigate to `Settings > Account Settings` page, where you can create or update your token.

This token provides read and write access to your account, so do not share or distribute it. Grant access only to those who need it. Ensure it is kept out of any version control system you may be using.
Do not use this API to publish your stories to any platform, as it is rate limited and your token will be exposed.


# Endpoints

```sh
curl \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    "https://api.storyly.io/api/story_group?token=your_token_here&filter=value"
```
> Make sure to replace `your_token_here` with your API token.

Storyly API base URL is: `https://api.storyly.io/api`

Currently available endpoints are:  `/story_group` `/story`

Token should be provided on query string of each API request, such as:
`https://api.storyly.io/api/story_group?token=your_token_here`

All post / patch request bodies should be in JSON format and `Content-Type: applicaton/json` should be added to request header.

Available filters and parameters (will be described in detail below) can be added to query string.


# Story Group

## Story Group Endpoints

```sh
https://api.storyly.io/api/story_group
```

Story Group Endpoint allows list, create, update and delete actions.


## Story Group Entity

```json
{
    "id": 1,
    "app_id": 1,
    "title": "Test Story Group",
    "icon": "https://db62cod6cnasq.cloudfront.net/user-media/1044/a6b1932c53fedeb801cb7a0d6c038be4.jpg",
    "target_cap": 1000,
    "pinned": 0,
    "sort_order": 1,
    "settings": null,
    "segments": ["segment1", "segment2"],
    "status": 1,
    "views": 5003,
    "ts_start": "2020-07-09 08:15:00",
    "ts_end": null,
    "ts_created": "2020-07-09 08:15:00",
    "ts_updated": "2020-07-09 08:15:00"
}
```

Parameter   | Type          | Description
---------   | -----------   | -----------
id          | integer       | Internal ID of the story group.
app_id      | integer       | Internal ID of the app this story group attached.
title       | string        | Title of the story group.
icon        | string        | URL of the story group icon.
target_cap  | integer       | Target view cap. Story group will be paused when view count reaches cap.
pinned      | boolean       | Pin status of the story group.
segments    | array         | An array of strings, your story groups will be segmented using these segments. Available in Storyly SDK 1.3.0 and later.
sort_order  | integer       | Order of the story group.
settings    | object        | Additonal story group settings.
status      | integer       | Status of the story group. Only ACTIVE story groups will be displayed by SDK.<br>Possible values: <br>`ACTIVE = 1`,<br>`PASSIVE = 2`,<br>`CAP_REACHED = 3`,<br>`END_DATE_REACHED = 4`,<br>`ARCHIVED = 9`
views       | integer       | View count of the story group. <br><small>Will be filled by system, do not post this field when creating / updating a story.</small>
ts_start    | date          | Start date of the story group. Story group will not be displayed by SDK if this date is not reached.
ts_end      | date          | End date of the story group. Story group will not be displayed by SDK after this date is reached. Set as `null` if you do not want to set an end date.
ts_created  | date          | Date story group was created. <br><small>Will be filled by system, do not post this field when creating / updating a story.</small>
ts_updated  | date          | Date story group was updated. <br><small>Will be filled by system, do not post this field when creating / updating a story.</small>

## Create a Story Group

```sh
curl \
    --header 'Content-Type: application/json' \
    --request POST \
    --data '{
        "app_id": 1,
        "title": "Test Story Group",
        "icon": "https://via.placeholder.com/250x250.jpg?text=StoryGroupIcon",
        "target_cap": null,
        "pinned": false,
        "segments": null,
        "sort_order": 1,
        "settings": null,
        "status": 1,
        "ts_start": "2020-07-09 08:15:00"
        "ts_end": null
    }' \
    'https://api.storyly.io/api/story_group?token=your_token_here'
```
Create a new story group on given storyly instance.

### HTTP Request

`POST https://api.storyly.io/api/story_group?token=your_token_here`

## Get a Specific Story Group

```sh
curl \
    --header 'Content-Type: application/json' \
    --request GET \
    'https://api.storyly.io/api/story_group/detail?token=your_token_here&id=150'
```

> The above command returns JSON structured like this:

```json
{
    "status": "ok",
    "message": "success",
    "data": {
        "id": 150,
        "app_id": 1,
        "title": "Test Story Group",
        "icon": "https://db62cod6cnasq.cloudfront.net/user-media/1044/a6b1932c53fedeb801cb7a0d6c038be4.jpg",
        "target_cap": 1000,
        "pinned": 0,
        "sort_order": 1,
        "settings": null,
        "segments": ["segment1", "segment2"],
        "status": 1,
        "views": 5003,
        "ts_start": "2020-07-09 08:15:00",
        "ts_end": null,
        "ts_created": "2020-07-09 08:15:00",
        "ts_updated": "2020-07-09 08:15:00"
    }
}
```

This endpoint retrieves a specific story group.

### HTTP Request

`GET https://api.storyly.io/api/story_group/detail?token=your_token_here&id=150`

### URL Parameters

Parameter   | Description
---------   | -----------
id          | The ID of the story group to retrieve

## List Story Groups

```sh
curl \
    --header 'Content-Type: application/json' \
    --request GET \
    'https://api.storyly.io/api/story_group?token=your_token_here'
```

> The above command returns JSON structured like this:

```json
{
    "status": "ok",
    "message": "success",
    "data": [
        {
            "id": 150,
            "app_id": 1,
            "title": "Test Story Group",
            "icon": "https://db62cod6cnasq.cloudfront.net/user-media/1044/a6b1932c53fedeb801cb7a0d6c038be4.jpg",
            "target_cap": 1000,
            "pinned": 0,
            "sort_order": 1,
            "settings": null,
            "segments": ["segment1", "segment2"],
            "status": 1,
            "views": 5003,
            "ts_start": "2020-07-09 08:15:00",
            "ts_end": null,
            "ts_created": "2020-07-09 08:15:00",
            "ts_updated": "2020-07-09 08:15:00"
        },
        {
            "id": 151,
            "app_id": 1,
            "title": "Test Story Group",
            "icon": "https://db62cod6cnasq.cloudfront.net/user-media/1044/a6b1932c53fedeb801cb7a0d6c038be4.jpg",
            "target_cap": 1000,
            "pinned": 0,
            "sort_order": 1,
            "settings": null,
            "segments": ["segment1", "segment2"],
            "status": 1,
            "views": 5003,
            "ts_start": "2020-07-09 08:15:00",
            "ts_end": null,
            "ts_created": "2020-07-09 08:15:00",
            "ts_updated": "2020-07-09 08:15:00"
        }, ...
    ]
}
```

This endpoint lists story groups.

### HTTP Request

`GET https://api.storyly.io/api/story_group/detail?token=your_token_here&id=150`


## Update a Specific Story Group

```sh
curl \
    --header 'Content-Type: application/json' \
    --request PATCH \
    --data '{
        "title": "Test Story Group",
        "icon": "https://via.placeholder.com/250x250.jpg?text=StoryGroupIcon",
        "target_cap": null,
        "pinned": false,
        "segments": null,
        "sort_order": 1,
        "settings": null,
        "status": 1,
        "ts_start": "2020-07-09 08:15:00"
        "ts_end": null
    }' \
    'https://api.storyly.io/api/story_group?token=your_token_here&id=150'
```

This endpoint updates a specific story group.

### HTTP Request

`PATCH https://api.storyly.io/api/story_group?token=your_token_here&id=150`

### URL Parameters

Parameter | Description
--------- | -----------
id        | The ID of the story group to update


## Delete a Specific Story Group

```sh
curl \
    --header 'Content-Type: application/json' \
    --request DELETE \
    'https://api.storyly.io/api/story_group?token=your_token_here&id=150'
```

This endpoint deletes a specific story group. Entities will be deleted permanently.

### HTTP Request

`DELETE https://api.storyly.io/api/story_group?token=your_token_here&id=150`

### URL Parameters

Parameter | Description
--------- | -----------
id        | The ID of the story group to update

# Story

## Story Endpoints

```sh
https://api.storyly.io/api/story
```

Story Endpoint allows list, create, update and delete actions.


## Story Entity

```json
{
    "id": 1000,
    "story_group_id": 150,
    "type": 1,
    "title": "Test Story",
    "sort_order": 1,
    "media": "https://db62cod6cnasq.cloudfront.net/user-media/1044/a6b1932c53fedeb801cb7a0d6c038be4.jpg",
    "media_raw": "https://db62cod6cnasq.cloudfront.net/user-media/1044/a6b1932c53fedeb801cb7a0d6c038be4.jpg",
    "mime_type": "image/jpeg",
    "target_cap": 1000,
    "button_text": "Click Here",
    "outlink": "https://google.com",
    "deep_link": "app://s=1",
    "settings": {},
    "status": 1,
    "views": 5000,
    "ts_start": "2020-07-09 08:15:00",
    "ts_end": null,
    "ts_created": "2020-07-09 08:15:00",
    "ts_updated": "2020-07-09 08:15:00"
}
```

Parameter       | Type          | Description
---------       | -----------   | -----------
id              | integer       | Internal ID of the story.
story_group_id  | integer       | Internal ID of the story group this story is attached.
type            | integer       | Media type of the story. 1 for image, 2 for video, 3 for template stories. <br><small>Will be filled by system, do not post this field when creating / updating a story.</small>
title           | string        | Title of the story.
sort_order      | integer       | Order of the story.
media           | string        | URL of the optimized media.
media_raw       | string        | URL of the original media.
mime_type       | string        | Mime Type of the media. `image/jpeg`, `video/mp4`.<br> <small>Will be filled by system, do not post this field when creating / updating a story.</small>
target_cap      | integer       | Target view cap. Story will be paused when view count reaches cap.
button_text     | string        | CTA Button text.
outlink         | string        | CTA Button link.
deep_link       | string        | Deep link of the story. <br><small>Will be filled by system, do not post this field when creating / updating a story.</small>
settings        | object        | Additonal story settings.
status          | integer       | Status of the story. Only ACTIVE stories will be displayed by SDK.<br>Possible values: <br>`ACTIVE = 1`<br>`PASSIVE = 2`<br>`PASSIVE_BY_STORY_GROUP = 3`<br>`END_DATE_REACHED = 4`<br>`CAP_REACHED = 5`<br>`WAITING_MEDIA_IMPORT = 6`<br>`FAILED_MEDIA_IMPORT = 7`<br>`ARCHIVED = 9`
views           | integer       | View count of the story. <br><small>Will be filled by system as story recieves impressions, do not post this field when creating / updating a story.</small>
ts_start        | date          | Start date of the story. Story will not be displayed by SDK if this date is not reached.
ts_end          | date          | End date of the story. Story will not be displayed by SDK after this date is reached. Set as `null` if you do not want to set an end date.
ts_created      | date          | Date story was created. <br><small>Will be filled by system, do not post this field when creating / updating a story.</small>
ts_updated      | date          | Date story was updated. <br><small>Will be filled by system, do not post this field when creating / updating a story.</small>

## Create a Story

```sh
curl \
    --header 'Content-Type: application/json' \
    --request POST \
    --data '{
        "story_group_id": 150,
        "title": "Test Story",
        "sort_order": 1,
        "media": "https://db62cod6cnasq.cloudfront.net/user-media/1044/a6b1932c53fedeb801cb7a0d6c038be4.jpg",
        "target_cap": 1000,
        "button_text": "Click Here",
        "outlink": "https://google.com",
        "settings": {},
        "status": 1,
        "ts_start": "2020-07-09 08:15:00",
        "ts_end": null
    }' \
    'https://api.storyly.io/api/story?token=your_token_here'
```
Create a new story on given story group.

### HTTP Request

`POST https://api.storyly.io/api/story?token=your_token_here`

## Get a Specific Story

```sh
curl \
    --header 'Content-Type: application/json' \
    --request GET \
    'https://api.storyly.io/api/story/detail?token=your_token_here&id=1000'
```

> The above command returns JSON structured like this:

```json
{
    "status": "ok",
    "message": "success",
    "data": {
        "id": 1000,
        "story_group_id": 150,
        "type": 1,
        "title": "Test Story",
        "sort_order": 1,
        "media": "https://db62cod6cnasq.cloudfront.net/user-media/1044/a6b1932c53fedeb801cb7a0d6c038be4.jpg",
        "media_raw": "https://db62cod6cnasq.cloudfront.net/user-media/1044/a6b1932c53fedeb801cb7a0d6c038be4.jpg",
        "mime_type": "image/jpeg",
        "target_cap": 1000,
        "button_text": "Click Here",
        "outlink": "https://google.com",
        "deep_link": "app://s=1",
        "settings": {},
        "status": 1,
        "views": 5000,
        "ts_start": "2020-07-09 08:15:00",
        "ts_end": null,
        "ts_created": "2020-07-09 08:15:00",
        "ts_updated": "2020-07-09 08:15:00"
    }
}
```

This endpoint retrieves a specific story.

### HTTP Request

`GET https://api.storyly.io/api/story/detail?token=your_token_here&id=150`

### URL Parameters

Parameter   | Description
---------   | -----------
id          | The ID of the story to retrieve

## List Stories

```sh
curl \
    --header 'Content-Type: application/json' \
    --request GET \
    'https://api.storyly.io/api/story?token=your_token_here'
```

> The above command returns JSON structured like this:

```json
{
    "status": "ok",
    "message": "success",
    "data": [
        {
            "id": 1000,
            "story_group_id": 150,
            "type": 1,
            "title": "Test Story",
            "sort_order": 1,
            "media": "https://db62cod6cnasq.cloudfront.net/user-media/1044/a6b1932c53fedeb801cb7a0d6c038be4.jpg",
            "media_raw": "https://db62cod6cnasq.cloudfront.net/user-media/1044/a6b1932c53fedeb801cb7a0d6c038be4.jpg",
            "mime_type": "image/jpeg",
            "target_cap": 1000,
            "button_text": "Click Here",
            "outlink": "https://google.com",
            "deep_link": "app://s=1",
            "settings": {},
            "status": 1,
            "views": 5000,
            "ts_start": "2020-07-09 08:15:00",
            "ts_end": null,
            "ts_created": "2020-07-09 08:15:00",
            "ts_updated": "2020-07-09 08:15:00"
        },
        {
            "id": 1001,
            "story_group_id": 150,
            "type": 1,
            "title": "Test Story",
            "sort_order": 1,
            "media": "https://db62cod6cnasq.cloudfront.net/user-media/1044/a6b1932c53fedeb801cb7a0d6c038be4.jpg",
            "media_raw": "https://db62cod6cnasq.cloudfront.net/user-media/1044/a6b1932c53fedeb801cb7a0d6c038be4.jpg",
            "mime_type": "image/jpeg",
            "target_cap": 1000,
            "button_text": "Click Here",
            "outlink": "https://google.com",
            "deep_link": "app://s=1",
            "settings": {},
            "status": 1,
            "views": 5000,
            "ts_start": "2020-07-09 08:15:00",
            "ts_end": null,
            "ts_created": "2020-07-09 08:15:00",
            "ts_updated": "2020-07-09 08:15:00"
        }, ...
    ]
}
```

This endpoint lists stories.

### HTTP Request

`GET https://api.storyly.io/api/story_group/detail?token=your_token_here`


## Update a Specific Story

```sh
curl \
    --header 'Content-Type: application/json' \
    --request PATCH \
    --data '{
        "title": "Test Story",
        "sort_order": 1,
        "target_cap": 1000,
        "button_text": "Click Here",
        "outlink": "https://google.com",
        "settings": {},
        "status": 1,
        "ts_start": "2020-07-09 08:15:00",
        "ts_end": null
    }' \
    'https://api.storyly.io/api/story?token=your_token_here&id=150'
```

This endpoint updates a specific story.

### HTTP Request

`PATCH https://api.storyly.io/api/story?token=your_token_here&id=150`

### URL Parameters

Parameter | Description
--------- | -----------
id        | The ID of the story to update

## Delete a Specific Story

```sh
curl \
    --header 'Content-Type: application/json' \
    --request DELETE \
    'https://api.storyly.io/api/story?token=your_token_here&id=150'
```

This endpoint deletes a specific story. Entities will be deleted permanently.

### HTTP Request

`DELETE https://api.storyly.io/api/story?token=your_token_here&id=150`