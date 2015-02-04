---
title: Create Channels
layout: default
category: Miscellaneous
permalink: v1_1_0-docs/channels/
---

Channels provide means to organize content into a single stream. The News interface, for example, provides different channels grouped by document category. We show news for business, economics, science, sports, etc.
Channels can be created/updated via `POST/PUT` request to the `/channels` endpoint, providing a JSON payload in the request body.

## Channel object

In order to understand how to build the JSON, you need to understand a bit more how the channels are represented in RDF. A channel in the JSON format has the following properties:

* uri - the instance id of the channel, must be a URI in order to map additional properties to it, such as name and index
* name - channel name (this string will be shown in the interface). To name a channel use the predicate `http://ontology.ontotext.com/publishing#hasName`.
* index - the order in the list of channels shown in the UI. To map an index to a channel use the predicate `http://ontology.ontotext.com/publishing#hasIndex`
* concepts - the document should contain all of the concepts in this list
* features - the document should have all the features with the values from the list
* categories - the document should have any of those categories. The categories values could be either a URI or a Literal and should be declared with the predicate `http://ontology.ontotext.com/publishing#hasCategory`

## Example

The following can be used to creates channels grouped by document category:

<pre>
```
[
    {
        "uri": "http://www.ontotext.com/publishing#International",
        "name": "International",
        "index": 0,
        "categories": [
          "International"
        ]
    }, {
        "uri": "http://www.ontotext.com/publishing#Business",
        "name": "Business",
        "index": 1,
        "categories": [
          "Business"
        ]
    }, {
        "uri": "http://www.ontotext.com/publishing#ScienceAndTechnology",
        "name": "Science and Technology",
        "index": 2,
        "categories": [
          "Science and Technology"
        ]
    }, {
        "uri": "http://www.ontotext.com/publishing#Sports",
        "name": "Sports",
        "index": 3,
        "categories": [
          "Sports"
        ]
    }, {
        "uri": "http://www.ontotext.com/publishing#Lifestyle",
        "name": "Lifestyle",
        "index": 4,
        "categories": [
          "Lifestyle"
        ]
    }
]

```</pre>



## Advanced filtering

Let's consider the following:

    {
        "uri": "http://www.ontotext.com/publishing#Channel-Musica",
        "name": "Music",
        "index": 0,
        "concepts": [
             "http://ontology.ontotext.com/resource/Nina_Simone",
             "http://ontology.ontotext.com/resource/Billie_Holiday"
         ],
        "features": [
            {
                "uri": "a:featureGenre",
                "name": "Genre",
                "value": "Jazz"
            },
            {
                "uri": "a:featureRegion",
                "name": "Region",
                "value": "US"
            }
        ],
        "categories": [
          "Music",
          "Culture"
        ]
    }

This channel will include documents that satisfy the following requirements:
* mention both "Nina Simone" and "Billie Holiday"
* have feature "Genre":"Jazz" and have feature "Region":"US"
* have either category "Music" or "Culture"
