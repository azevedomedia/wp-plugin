# CUSTOM WORDPRESS PLUGIN
 - WP Remote Administrator

- - -

> Sumary

- 1.0 About the plugin
- 2.0 Insert .JSON Example
- 3.0 Explain the data nodes
    - 3.1. "Action" (required)
    - 3.2. "External id" (required)
    - 3.3. "Type" (required)
    - 3.4. "Comment Status"
    - 3.5. "Featured Image"
    - 3.6. "Title" (required)
    - 3.7. "Slug" (required)
    - 3.8. "Excerpt"
    - 3.9. "Content"
        - 3.9.1 "Content Media"
    - 3.10. "Taxonomies"
    - 3.11. "Fields"
 
 - - -

# 1. About the plugin

> This plugin will works as a "bridge" before the "rest-api" (v2)" and "oauth" (v2) plugins for any remote situation of data manipulation described in the project. After processing the data, the plugin will trigger the Wordpress API functions according to the request:

  - Insert
  - Update
  - Delete

# 2. Insert .JSON Example

```
{
    "action" : "insert",
    "external-id" : 1111,

    "type": "post",
    "comment" : "open",

    "featured_image": {
        "url": "http://publicdomain.xyz/media-file.xyz",
        "title": "Post Title",
        "content": "Media Description",
        "excerpt": "Alternate Image Text",
    }

    "title": "The Post Title",
    "name": "the-post-title",
    "excerpt": "Loren Lipsum Loren",

    "content": "<html><body><p>Loren Lipsum Loren</p><img src="http://publicdomain.xyz/media-file-1.xyz" height="50" width="50"> <img src="http://publicdomain.xyz/media-file-2.xyz" height="50" width="50"></body></html>", 
    "content_media": [
        {
            "url": "http://publicdomain.xyz/media-file-1.xyz",
            "title": "Post Title 1",
            "content": "Media Description",
            "excerpt": "Alternate Image Text"
        },
        {
            "url": "http://publicdomain.xyz/media-file-2.xyz",
            "title": "Post Title 2",
            "content": "Media Description 2",
            "excerpt": "Alternate Image Text 2"
        }
    ]

    "taxonomies": [
        {
            "type": "category",
            "name": "Category 1",
            "slug": "category-1",
            "description": "Optional description of the taxonomy displayed in the template.",
        },
        {
            "type": "category",
            "name": "Category 2",
            "slug": "category-2",
            "description": "Optional description of the taxonomy displayed in the template.",
            "parent": "Category 1",
        },
        {
            "type": "post_tag",
            "name": "Tag 1",
            "slug": "tag-1"
            "parent": "",
            "description": "",
        }
        {
            "type": "custom_taxonomy",
            "name": "Custom Taxonomy 1",
            "slug": "Custom-taxonomy-1"
            "parent": "",
            "description": "",
        }
    ]

    "custom_fields": [
        {
            "key": "gallery-1",
            "value": [
                {
                    "url": "http://publicdomain.xyz/media-file-1.xyz",
                    "title": "Post Title 1",
                    "content": "Media Description",
                    "excerpt": "Alternate Image Text",
                },
                {
                    "url": "http://publicdomain.xyz/media-file-2.xyz",
                    "title": "Post Title 2",
                    "content": "Media Description 2",
                    "excerpt": "Alternate Image Text 2",
                }
            ]
        },
        {
            "key": "gallery-2",
            "value": [
                {
                    "url": "http://publicdomain.xyz/media-file-3.xyz",
                    "title": "Post Title 1",
                    "content": "Media Description",
                    "excerpt": "Alternate Image Text",
                },
            ]
        },
        {
            "key": "anything-x",
            "value": "Content Value X",
        },
        {
            "key": "anything-y",
            "value": "Content Value Y",
        },
        {
            "key": "anything-z",
            "value": "Content Value Z",
        },
    ]
}
```

# 3. Explain the data nodes:

In case of INSERT, the data are partitioned in these parts:

# 3.1. "Action" (required)
> Options: "insert", "update" or "delete"

Example:

```
    {
    "action" : "insert",
    }
```

# 3.2. "External id" (required)
>  The post reference in the source system where the content was created.

Example:

```
    {
    "external_id" : 1111,
    }
```

# 3.3. "Type" (required)
>  Any post types created according to project demand where "post" is the default post type on Wordpress.

Example:

```
    {
    "type" : places,
    }
```
  
# 3.4. "Comment Status"

>  If the status is "open" accept comments. The default is "closed".

Example:

```
    {
    "comment" : "open",
    }
```

# 3.5. "Featured Image"

>  The featured image of the post has 4 parameters. The required field is "media_url". The optional fields (important for SEO) are: "media_title",    "media_description" and "media_alternate_text". The media needs to be in an accessible url.

Example:

```
    "featured_image": {
        "url": "http://publicdomain.xyz/media-file.xyz",
        "title": "Media Title",
        "description": "Media Description",
        "alternate_text": "Alternate Media Text",
    }
```
  
# 3.6. "Title" (required)

>  The title of the post.

Example:

```
    "title": "The Post Title",
```

# 3.7. "Slug" (required)

>  The post slug is the user friendly and URL valid name (permalink) of a post.

Example:

```
    "slug": "the-post-title-with-an-cool-name-for-a-good-seo",
```
  
# 3.8. "Excerpt"

>  This excerpt of the content is used for feeds on the pages that list the posts. This field needs to be sent in a HTML-encoded string.

Decoded example: 

```
    "excerpt": "<p>some text</p>, 'sampler'",
```

Encoded example (send in this format): 

```
    "excerpt": "&#x3C;p&#x3E;some text&#x3C;/p&#x3E;, &#x27;sampler&#x27;",
```

# 3.9. "Content"

>  This is the "long text" field that some posts like articles have, usually with html formatting. This field needs to be sent in a HTML-encoded string. If the content have embeded content (example: images, pdf) the media needs to be in an accessible url.

Decoded example: 

```
    "content": "<html><body><p>Loren Lipsum Loren</p><img src="http://publicdomain.xyz/media-file-1.xyz" height="50" width="50"> <img src="http://publicdomain.xyz/media-file-2.xyz" height="50" width="50"></body></html>",
```

Encoded example (send in this format): 

```
    "content": "&#x3C;html&#x3E;&#x3C;body&#x3E;&#x3C;p&#x3E;Loren Lipsum Loren&#x3C;/p&#x3E;&#x3C;img src=&#x22;http://publicdomain.xyz/media-file-1.xyz&#x22; height=&#x22;50&#x22; width=&#x22;50&#x22;&#x3E; &#x3C;img src=&#x22;http://publicdomain.xyz/media-file-2.xyz&#x22; height=&#x22;50&#x22; width=&#x22;",
```

# 3.9.1 "Content Media"

>  This node is recommended (SEO) if the above field "content" has any image inserted. They should be listed here (in a array) with complete SEO data. *The media needs to be in an accessible url.

Example (2 medias): 

```
     "content_media": [
        {
            "url": "http://publicdomain.xyz/media-file-1.xyz",
            "title": "Post Title 1",
            "description": "Media 1 Description",
            "alternate_text": "Alternate Media 1 Text",
        },
        {
            "url": "http://publicdomain.xyz/media-file-2.xyz",
            "title": "Post Title 2",
            "description": "Media 2 Description",
            "alternate_text": "Alternate Media 2 Text",
        }
    ]
```
  
# 3.10. "Taxonomies"

>  Any post can have one or more taxonomy (category, tag are two examples of this). Taxonomies should be entered informing the "type", "name", "slug", an optional "description" and a "parent" taxonomy, also optional (In this case enter the "title" of the parent taxonomy). Send all taxonomies in an array node.

Example (1 tag, 2 category, 3 category with parent, 4 custom):

```
    "taxonomies": [
        {
            "type": "tag",
            "name": "Tag 1",
            "slug": "tag-1",
        },
        {
            "type": "category",
            "name": "Category 1",
            "slug": "category-1",
        },
        {
            "type": "category",
            "name": "Category 2",
            "slug": "category-2"
            "parent": "Category 1",
            "description": "",
        },
        {
            "type": "custom",
            "name": "Custom Taxonomy 1",
            "slug": "Custom-taxonomy-1",
            "parent": "",
            "description": "",
        }
    ]
```

# 3.11. "Custom Fields"

>  Any non-standard data (title, short text, long text, taxonomies) of a Wordpress post is considered a custom field. Each type of post can have different types of custom fields. Custom fields contain a description and a value, which can be a parameter or a set of values in a vector. In the Wordpress template, these fields are used as designed. Send all taxonomies in an array node. If the data is an media url it will be imported into the Wordpress media library, to send the SEO data from this media create a child node with this data.

Example 1 (Single custom fields in an array):

```
    "custom_fields": [
        {
            "key": "anything-x",
            "value": "Content Value X",
        },
        {
            "key": "anything-y",
            "value": "Content Value Y",
        },
        {
            "key": "anything-z",
            "value": "Content Value Z",
        },
    ]
```

Example 2 (Custom fields with a photo gallery and media's metadata on child nodes):

```
    "custom_fields": [
        {
            "key": "gallery-1",
            "value": [
                {
                    "url": "http://publicdomain.xyz/media-file-1.xyz",
                    "title": "Post Title 1",
                    "description": "Media 1 Description",
                    "alternate_text": "Alternate Media 1 Text",
                },
                {
                    "url": "http://publicdomain.xyz/media-file-2.xyz",
                    "title": "Post Title 2",
                    "description": "Media 2 Description",
                    "alternate_text": "Alternate Media 2 Text",
                }
            ]
        },
        {
            "key": "gallery-2",
            "value": [
                {
                    "url": "http://publicdomain.xyz/media-file-3.xyz",
                    "title": "Post Title 3",
                    "description": "Media 3 Description",
                    "alternate_text": "Alternate Media 3 Text",
                },
            ]
        },
    ]
```
