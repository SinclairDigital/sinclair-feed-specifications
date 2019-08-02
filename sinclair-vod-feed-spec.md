# Sinclair External VOD Feed

### Overview

This guide includes detailed information on the Sinclair External VOD Feed Specification, which can be used to build a content feed that includes movies, series, TV Specials, and/or short-form videos.

Initially, a JSON format will be supported that follows the JSON-Schema Draft 4. All the properties in the schema are **case sensitive**.

Before submitting a feed, make sure it is a valid JSON file. You can easily do that by using an IDE, or free online tools like [JSON Scheme Validator](http://www.jsonschemavalidator.net/) or [JSON Schema Linter](http://jsonschemalint.com/draft4/).

**Sections:**
* [JSON Feed Schema](#json-feed-schema)

**Content types:**
* [movie](#movie)
* [series](#series)
* [season](#season)
* [episode](#episode)
* [shortFormVideo](#shortformvideo)
* [tvSpecial](#tvspecial)

**Content categorization:**
* [playlist](#playlist)

**Content properties:**
* [content](#content)
* [video](#video)
* [caption](#caption)
* [trickPlayFile](#trickplayfile)
* [genres](#genres)
* [tag](#tag)
* [group](#group)
* [thumbnail](#thumbnail)
* [externalId](#externalid)
* [rating](#rating)
* [Parental Ratings](#parental-ratings)
* [Rating Sources](#rating-sources)
* [adbreak](#adbreak)
* [credit](#credit)

---

## JSON Feed Schema
These are the properties for the root object of your feed. It contains basic information such as your company's name, when the feed was last updated, and other objects that will describe all your content such as TV Shows, Movies, etc.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| feedVersion | string | Required | The version of the feed specification.
| wurlChannelSlug | string | Required | A channel identifier that can be used to query the Wurl API for additional channel meta data.
| providerName | string | Required | The name of the feed provider. E.g.: “Acme Productions”.
| lastUpdated | string | Required | The date that the feed was last modified in the [ISO 8601](http://www.iso.org/iso/home/standards/iso8601.htm) format: {YYYY}-{MM}-{DD}T{hh}:{mm}:{ss}+{TZ}. E.g.: 2015-11-11T22:21:37+00:00
| language | string | Required | The language the channel uses for all its information and descriptions. (e.g., “en”, “en-US”, “es”, etc.). ISO 639 alpha-2 or alpha-3 language code string.
| movies | [Movie Object](#movie) | Required* | A list of one or more movies.
| series | [Series Object](#series) | Required* | A list of one or more series. Series are episodic in nature and would include TV shows, daily/weekly shows, etc.
| shortFormVideos | [ShortFormVideo Object](#shortformvideo) | Required* | A list of one or more short-form videos. Short-form videos are usually less than 20 minutes long and are not TV Shows or Movies.
| tvSpecials | [TV Special Object](#tvspecial) | Required* | A list of one or more TV Specials. TV Specials are one-time TV programs that are not part of a series.
| playlists | [Playlist Object](#playlist) | Optional | A list of one or more playlists.

> :information_source: *At least one of these content types is required

Feed Root Object Example:

```json
{
    "feedVersion": "0.1",
    "providerName": "Wurl Productions",
    "wurlChannelSlug": "alt_channel",
    "lastUpdated": "2017-11-11T22:21:37+00:00",
    "language": "en",
    "playlists": [
        ...
    ],
    "movies": [
        ...
    ],
    "series": [
        ...
    ],
    "shortFormVideos":  [
        ...
    ],
    "tvSpecials": [
        ...
    ]
}
```

---

## movie
Child object of root property `movies`.

This object represents a movie object.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| id | string | Required | Your immutable string reference ID for the movie. THIS CANNOT CHANGE. This should serve as a unique identifier for the movie across different locales.
| title | string | Required | Movie title. Please use plain text and don’t include extra information like year, version label, etc.
| content | [Content Object](#content) | Required | The actual video content, such as the URL of the video file, subtitles, etc.
| thumbnails | [Thumbnail Object](#thumbnail) | Required | One or more thumbnails. Must include one thumbnail with at least 1280x720 resolution. Must include one thumbnail with at least 1280x720 resolution.
| releaseDate | string | Required | The date the movie was initially released or first aired. Conforms to the [ISO 8601](http://www.iso.org/iso/home/standards/iso8601.htm) format: {YYYY}-{MM}-{DD}. E.g.: 2015-11-11
| shortDescription | string | Required | A description that does not exceed 200 characters.
| longDescription | string | Optional | A longer description exceeding 200.
| tags | [Tag Object](#tag) | Optional | One tag object.
| credits | [Credit Object](#credit) | Optional | One or more credits. The cast and crew of the movie.
| ratings | [Rating Object](#rating) | Optional | One or more parental ratings for the content.
| externalIds | [External ID Object](#externalid) | Optional | One or more third-party metadata provider IDs.

Movie Object Example:

```json
{
    "id": "1509428502952",
    "title": "Sample Movie",
    "content": {
        ...
    },
    "releaseDate": "2016-01-01",
    "shortDescription": "Incredible movie description",
    "longDescription": "Even more incredible and longer movie description",
    "tags": {
      "genres": [
        "genre 1",
        "genre 2"
      ],
      "keywords": [
        "keyword 1",
        "keyword 2"
      ],
      "categories": [
        "category 1",
        "category 2"
      ]
    },
    "thumbnails": [
      {
        "name": "default",
        "width": 1280,
        "height": 720,
        "url": "http://static.channels.com/thumbnails/show123-defult.png"
      },
      {
        "name": "hero",
        "width": 1920,
        "height": 1080,
        "url": "http://static.channels.com/thumbnails/show123-hero.png"
      }
    ],
    "ratings": [
      {
        "rating": "PG",
        "ratingSource": "USA_PR"
      }
    ]
}
```

---


## series
Child object of root property `series`.

This object represents a series, such as a season of a TV Show or a mini-series.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| id | string | Required | Your immutable string reference ID for the series. THIS CANNOT CHANGE. This should serve as a unique identifier for the movie across different locales.
| title | string | Required | The title of the series.
| |
| seasons | [Season Object](#season) | Required* | One or more seasons of the series. Seasons should be used if episodes are grouped by seasons.
| episodes | [Episode Object](#episode) | Required* | One or more episodes of the series. Episodes should be used if they are not grouped by seasons (e.g., a mini-series).
| |
| thumbnails | [Thumbnail Object](#thumbnail) | Required | One or more thumbnails. Must include one thumbnail with at least 1280x720 resolution.  Must include one thumbnail with at least 1280x720 resolution.
| releaseDate | string | Required | The date the series first aired. Conforms to the [ISO 8601](http://www.iso.org/iso/home/standards/iso8601.htm) format: {YYYY}-{MM}-{DD}. E.g.: 2015-11-11
| shortDescription | string | Required | A description that does not exceed 200 characters.
| longDescription | string | Optional | A longer description exceeding 200.
| tags | [Tag Object](#tag) | Optional | One tag object.
| groups | [Group Object](#group) | Optional | An array of groups (episodes grouped together).
| credits | [Credit Object](#credit) | Optional | One or more credits. The cast and crew of the series.
| ratings | [Rating Object](#rating) | Optional | One or more parental ratings for the content.
| externalIds | [External ID Object](#externalid) | Optional | One or more third-party metadata provider IDs.

> :information_source: *Must have either `seasons` or `episodes`

Series Object Example (seasons):

```json
{
  "id": "1509428502952",
  "title": "The Amazing Series with Seasons!",
  "seasons": [
    ...
  ],
  "shortDescription": "Wondrous series seasons.",
  "groups": {
    ...
  },
  "tags": {
      "genres": [
        "genre 1",
        "genre 2"
      ],
      "keywords": [
        "keyword 1",
        "keyword 2"
      ],
      "categories": [
        "category 1",
        "category 2"
      ]
    },
    "thumbnails": [
      {
        "name": "default",
        "width": 1280,
        "height": 720,
        "url": "http://static.channels.com/thumbnails/show123-defult.png"
      },
      {
        "name": "hero",
        "width": 1920,
        "height": 1080,
        "url": "http://static.channels.com/thumbnails/show123-hero.png"
      }
    ]
}
```

Series Object Example (mini-series):

```json
{
  "id": "1509428502952",
  "title": "The Amazing Series with Episodes Only!",
  "episodes": [
    ...
  ],
  "groups": [
    ...
  ],
  "thumbnails": [
    {
      "name": "default",
      "width": 1280,
      "height": 720,
      "url": "http://static.channels.com/thumbnails/show123-defult.png"
    },
    {
      "name": "hero",
      "width": 1920,
      "height": 1080,
      "url": "http://static.channels.com/thumbnails/show123-hero.png"
    }
  ],
  "shortDescription": "Unbelievables series episodes."
}
```

---

### season
Child object of property `series` -> `seasons`.

This object represents a single season of a series.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| seasonNumber | integer | Required | Sequential season number. E.g.: 3 or 2015.
| episodes | [Episode Object](#episode) | Required | One or more episodes of this particular season.
| seasonTitle | string | Optional | The season title.
| thumbnails | [Thumbnail Object](#thumbnail) | Optional | One or more thumbnails. Must include one thumbnail with at least 1280x720 resolution.  Must include one thumbnail with at least 1280x720 resolution.
| groups | [Group Object](#group) | Optional | An array of groups (episodes grouped together).

Season Object Example:

```json
{
  "seasonNumber": "1",
  "seasonTitle": "Go forward!",
  "episodes": [
    ...
  ],
  "groups": [
    ...
  ]
}
```

---

### episode
Child object of property:

* `series` -> `episodes`
* `series` -> `seasons` -> `episodes`

This object represents a single episode in a series or a season.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| id | string | Required | Your immutable string reference ID for the episode. THIS CANNOT CHANGE. This should serve as a unique identifier for the movie across different locales.
| title | string | Required | Episode title. Please don’t include extra information like year, version label, etc.
| content | [Content Object](#content) | Required | The actual video content, such as the URL of the video file, subtitles, etc.
| thumbnails | [Thumbnail Object](#thumbnail) | Required | One or more thumbnails. Must include one thumbnail with at least 1280x720 resolution.
| episodeNumber | integer | Required | The sequential episode number. E.g.: 3.
| releaseDate | string | Required | The date the episode first aired. Conforms to the [ISO 8601](http://www.iso.org/iso/home/standards/iso8601.htm) format: {YYYY}-{MM}-{DD}. E.g.: 2015-11-11
| shortDescription | string | Required | A description that does not exceed 200 characters.
| longDescription | string | Optional | A longer description exceeding 200.
| tags | [Tag Object](#tag) | Optional | One tag object.
| credits | [Credit Object](#credit) | Optional | One or more credits. The cast and crew of the episode.
| ratings | [Rating Object](#rating) | Optional | One or more parental ratings for the content.
| externalIds | [External ID Object](#externalid) | Optional | One or more third-party metadata provider IDs.

Episode Object Example:

```json
{
  "id": "1509428502952",
  "title": "The Amazing First Episode Title",
  "content": {
    ...
  },
  "thumbnails": [
    {
      "name": "default",
      "width": 1280,
      "height": 720,
      "url": "http://static.channels.com/thumbnails/show123-defult.png"
    },
    {
      "name": "hero",
      "width": 1920,
      "height": 1080,
      "url": "http://static.channels.com/thumbnails/show123-hero.png"
    }
  ],
  "episodeNumber": 1,
  "shortDescription": "Marvelous episode description",
  "tags": {
      "genres": [
        "genre 1",
        "genre 2"
      ],
      "keywords": [
        "keyword 1",
        "keyword 2"
      ],
      "categories": [
        "category 1",
        "category 2"
      ]
    }

}
```

---

## shortFormVideo
Child object of root property `shortFormVideos`.

Short-form videos are generally less than 20 minutes long, and are not TV Shows or Movies.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| id | string | Required | Your immutable string reference ID for the video. THIS CANNOT CHANGE. This should serve as a unique identifier for the movie across different locales.
| title | string | Required | Video title. Please don’t include extra information like year, version label, etc.
| content | [Content Object](#content) | Required | The actual video content, such as the URL of the video file, subtitles, etc.
| thumbnails | [Thumbnail Object](#thumbnail) | Required | One or more thumbnails. Must include one thumbnail with at least 1280x720 resolution.
| shortDescription | string | Required | A description that does not exceed 200 characters.
| longDescription | string | Optional | A longer description exceeding 200.
| releaseDate | string | Required | The date the video first became available. Optional but very important, we recommend that you provide this. Conforms to the [ISO 8601](http://www.iso.org/iso/home/standards/iso8601.htm) format: {YYYY}-{MM}-{DD}. E.g.: 2015-11-11
| tags | [Tag Object](#tag) | Optional | One tag object.
| credits | [Credit Object](#credit) | Optional | One or more credits. The cast and crew of the video.
| ratings | [Rating Object](#rating) | Optional | One or more parental ratings for the content.

Short-form Video Object Example:

```json
{
  "id": "1509428502952",
  "title": "The Amazing Short-form Video",
  "content": {
    ...
  },
  "thumbnails": [
    {
      "name": "default",
      "width": 1280,
      "height": 720,
      "url": "http://static.channels.com/thumbnails/show123-defult.png"
    },
    {
      "name": "hero",
      "width": 1920,
      "height": 1080,
      "url": "http://static.channels.com/thumbnails/show123-hero.png"
    }
  ],
  "shortDescription": "Astonishing short-form video",
  "releaseDate": "2016-01-01",
  "tags": {
      "genres": [
        "genre 1",
        "genre 2"
      ],
      "keywords": [
        "keyword 1",
        "keyword 2"
      ],
      "categories": [
        "category 1",
        "category 2"
      ]
    }
}
```

---

## tvSpecial
Child object of root property `tvSpecials`.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| id | string | Required | Your immutable string reference ID for the TV Special. THIS CANNOT CHANGE. This should serve as a unique identifier for the movie across different locales.
| title | string | Required | Episode title. Please don’t include extra information like year, version label, etc.
| content | [Content Object](#content) | Required | The actual video content, such as the URL of the video file, subtitles, etc.
| thumbnails | [Thumbnail Object](#thumbnail) | Required | One or more thumbnails. Must include one thumbnail with at least 1280x720 resolution.
| releaseDate | string | Required | The date the TV Special first aired. Conforms to the [ISO 8601](http://www.iso.org/iso/home/standards/iso8601.htm) format: {YYYY}-{MM}-{DD}. E.g.: 2015-11-11
| shortDescription | string | Required | A description that does not exceed 200 characters.
| longDescription | string | Optional | A longer description exceeding 200.
| credits | [Credit Object](#credit) | Optional | One or more credits. The cast and crew of the TV special.
| ratings | [Rating Object](#rating) | Optional | One or more parental ratings for the content.
| tags | [Tag Object](#tag) | Optional | One tag object.
| externalIds | [External ID Object](#externalid) | Optional | One or more third-party metadata provider IDs.

TV Special Object Example:

```json
{
  "id": "1509428502952",
  "title": "The Amazing First Episode Title",
  "content": {
    ...
  },
  "thumbnails": [
    {
      "name": "default",
      "width": 1280,
      "height": 720,
      "url": "http://static.channels.com/thumbnails/show123-defult.png"
    },
    {
      "name": "hero",
      "width": 1920,
      "height": 1080,
      "url": "http://static.channels.com/thumbnails/show123-hero.png"
    }
  ],
  "shortDescription": "Unusual episode description",
  "tags": {
      "genres": [
        "genre 1",
        "genre 2"
      ],
      "keywords": [
        "keyword 1",
        "keyword 2"
      ],
      "categories": [
        "category 1",
        "category 2"
      ]
    }
}
```

---

## playlist
Child object of root property `playlists`.

A playlist is an **ordered** list of videos that may contain a mix of [Movies](#movie), [Series](#series), [Short-form videos](#shortformvideo), and [TV Specials](#tvspecial). It references a list of video IDs that are defined elsewhere in the feed. The same video can be referenced in multiple playlists.

Playlists let you manually specify the order of the content, and so they are perfect, for example, to create a "Featured" category in your channel.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| name | string | Required | The name of the playlist. The name is limited to 20 characters.
| itemIds | string | Required | An ordered list of one or more item IDs. An item ID is the ID of a movie/series/short-form video/TV special.

Playlist Object Example:

```json
{
    "name": "featured content",
    "itemIds": [
        "1509428502952",
        "1509428502953",
        "1509428502954"
    ]
}
```

---

## content
Child object of property:

* `movie`
* `series` -> `episodes` -> `episode`
* `series` -> `seasons` -> `episodes` -> `episode`
* `shortFormVideo`
* `tvSpecial`

This object represents the details about a single video content of a movie, episode, short-form video, or TV special.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| dateAdded | string | Required | The date the video was added to the library in the [ISO 8601](http://www.iso.org/iso/home/standards/iso8601.htm) format: {YYYY}-{MM}-{DD}T{hh}:{mm}:{ss}+{TZ}. E.g.: 2015-11-11T22:21:37+00:00 This information is used to generate the “Recently Added” category.
| videos | [Video Object](#video) | Required | One or more video files. For non-adaptive streams, you can specify the same video with different qualities.
| duration | integer | Required | Runtime in seconds.
| captions | [Caption Object](#caption) | Optional
| trickPlayFiles | [Trickplay File Object](#trickplayfile) | Optional | The trickplay file(s) that displays images as a user scrubs through a video. Trickplay files in multiple qualities can be provided.
| language | string | Optional | The language in which the video was originally produced (e.g., “en”, “en-US”, “es”, etc). ISO 639 alpha-2 or alpha-3 language code string.
| validityPeriodStart | string | Optional | The date when the content should become available in the [ISO 8601](http://www.iso.org/iso/home/standards/iso8601.htm) format: {YYYY}-{MM}-{DD}T{hh}:{mm}:{ss}+{TZ}. E.g.: 2015-11-11T22:21:37+00:00
| validityPeriodEnd | string | Optional | The date when the content is no longer available in the [ISO 8601](http://www.iso.org/iso/home/standards/iso8601.htm) format: {YYYY}-{MM}-{DD}T{hh}:{mm}:{ss}+{TZ}. E.g.: 2015-11-11T22:21:37+00:00
| adBreaks | [Ad Break Object](#adbreak) | Optional | One or more time codes. Represents a time duration from the beginning of the video where an ad shows up. Conforms to the format: {hh}:{mm}:{ss}.

Content Object Example:

```json
{
  "dateAdded": "2015-11-11T22:21:37+00:00",
  "videos": [
    ...
  ],
  "trickPlayFiles": [
    ...
  ],
  "duration": 1290,
  "adBreaks": [
    {
      "name": "Ad 1",
      "cuePoint": 781.6266699999999,
      "duration": 120
    },
    {
      "name": "Ad 2",
      "cuePoint": 1561.7853389989998,
      "duration": 120
    }
  ]
}
```

---

### video
Child object of property `content` -> `videos`.

This object represents the details of a single video file.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| url | string | Required | The URL of the video itself. The video should be served from a CDN (Content Distribution Network). Supported formats are described in ...TODO.
| quality | enum | Required | Must be one of the following:<ul><li>HD – 720p</li><li>FHD – 1080p</li><li>UHD – 4K</li></ul>If your stream uses an adaptive bitrate, set the quality to the highest available.
| videoType | enum | Required | Must be one of the following:<ul><li>HLS</li><li>SMOOTH</li><li>DASH</li><li>MP4</li><li>MOV</li><li>M4V</li></ul>
| bitrate | integer | Required only for non-ABR streams. | The bitrate in kbps. For non-adaptive streams, this must be provided. It is not needed for an ABR (e.g., HLS) stream.

Video Object Example:

```json
{
  "url": "https://example.org/cdn/videos/1509428502952",
  "quality": "UHD",
  "videoType": "HLS"
}
```

---

### caption
Child object of property `content` -> `captions`.

This object represents a single video caption file of a video content.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| url | string | Required | The URL of the video caption file.
| language | string | Required | A language code for the subtitle (e.g., “en”, “es-mx”, “fr”, etc). [ISO 639-2 or alpha-3](https://www.loc.gov/standards/iso639-2/php/code_list.php) language code string.
| captionType | enum | Required | A string specifying the type of caption. Default is subtitle. Must be one of the following:<ul><li>CLOSED_CAPTION</li><li>SUBTITLE</li></ul>

Caption File Object Example:

```json
{
  "url": "https://example.org/cdn/subtitles/1509428502952/sub-fr.srt",
  "Language": "fr",
  "captionType": "CLOSED_CAPTION"
}
```

---

### trickPlayFile
Child object of property `content` -> `trickPlayFiles`.

This object represents a single trickplay file. Trickplay files are the images shown when a user scrubs through a video, either fast-forwarding or rewinding.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| url | string | Required | The URL to the image representing the trickplay file
| quality | enum | Required | Must be one of the following:<ul><li>HD – 720p</li><li>FHD – 1080p</li></ul>

Trickplay File Object Example:

```json
{
  "url": "https://example.org/cdn/trickplayFiles/1509428502952/1",
  "quality": "FHD"
}
```

---

## Genres

The following genres are supported:

* action
* adventure
* animals
* animated
* anime
* children
* comedy
* crime
* documentary
* drama
* educational
* fantasy
* faith
* food
* fashion
* gaming
* health
* history
* horror
* miniseries
* mystery
* nature
* news
* reality
* romance
* science
* science fiction
* sitcom
* special
* sports
* thriller
* technology

---

## externalId
Child object of property:

* `movie`
* `series`
* `series` -> `episodes` -> `episode`
* `series` -> `seasons` -> `episodes` -> `episode`
* `shortFormVideo`
* `tvSpecial`

This object represents a third-party metadata provider ID (such as TMS, Rovi, IMDB, EIDR), that can provide more information about a specific video content.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| id | string | Required | The third-party metadata provider ID for your video content. For example, in the case of IMDB you would use the last part of the URL of a movie such as "http://www.imdb.com/title/tt0371724".
| idType | enum | Required | Must be one of the following:<ul><li>TMS – A Tribune Metadata Service ID for the content</li><li>ROVI - A Rovi ID for the content</li><li>IMDB – An Internet Movie Database ID</li><li>EIDR – An Entertainment Identifier Registry ID</li></ul>

External ID Object Example:

```json
{
  "id": "tt0371724",
  "idType": "IMDB"
}
```

---

## thumbnail
Child object of property:

* `movie`
* `series`
* `shortFormVideo`
* `tvSpecial`

This object represents the thumbnail info.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| name | string | Required | The name of the thumbnail
| width | integer | Required | The width of the thumbnail
| height | integer | Required | The height of the thumbnail
| url | string | Required | The url of the thumbnail

Thumbnail Object Example:

```json
{
  "thumbnails": [
    {
      "name": "default",
      "width": 1280,
      "height": 720,
      "url": "http://static.channels.com/thumbnails/show123-defult.png"
    },
    {
      "name": "hero",
      "width": 1920,
      "height": 1080,
      "url": "http://static.channels.com/thumbnails/show123-hero.png"
    }
  ]
}
```

---

## tag
Child object of property:

* `movie`
* `series`
* `shortFormVideo`
* `tvSpecial`

This object represents the tagging info.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| genres | enum | Optional | An array of genres
| keywords | enum | Optional | An array of keywords
| categories | enum | Optional | An array of categories

Tag Object Example:

```json
{
  "genres": ["gaming", "technology"],
  "keywords": ["gamescoop"],
  "categories": ["foo", "bar"]
}
```

---

## group
Child object of property:

* `season`
* `series`

This object represents an episode grouping.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| name | string | Required | The name of the group.
| episodes | enum | Required | An array of episodes

Group Object Example:

```json
{
"groups": [
  {
    "name": "demo",
    "episodes": [
      {
        "id": "1408-0",
        "title": "Episode title",
        "content": {
          "dateAdded": "2018-06-05T16:00:27+0000",
          "videos": [
            {
              "url": "https://somesite.com/playlist.m3u8",
              "quality": "HD",
              "videoType": "HLS"
            }
          ],
          "duration": 2940,
          "captions": null,
          "language": "en-US",
          "adBreaks": "00:25:40"
        },
        "thumbnails": [
          {
            "name": "hero",
            "width": 1920,
            "height": 1080,
            "url": "http://somecdn.com/thumbnails/episode.png"
          }
        ],
        "episodeNumber": "1",
        "releaseDate": "2018-06-05",
        "shortDescription": "",
        "longDescription": "",
        "credits": null,
        "ratings": [
          {
            "rating": "PG",
            "ratingSource": "USA_PR"
          }
        ],
        "externalIds": null,
        "tags": {
          "genres": ["genre 1", "genre 2"],
          "keywords": [],
          "categories": []
        }
      }
    ]
}

```

---

## rating
Child object of property:

* `movie`
* `series` -> `episodes` -> `episode`
* `shortFormVideo`
* `tvSpecial`

This object represents the rating for the video content. You can define the parental rating, as well as the source (USA Parental Rating, UK Content Provider, etc). See [Parental Ratings](#parental-ratings) and [Rating Sources](#rating-sources) for acceptable values.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| rating | enum | Required | Must be a value listed in [Parental Ratings](#parental-ratings)
| ratingSource | enum | Required | Must be one of the following:<ul><li>BBFC</li><li>CHVRS</li><li>CPR</li><li>MPAA</li><li>UK_CP</li><li>USA_PR</li></ul>See [Rating Sources](#rating-sources) for more information.

Rating Object Example:

```json
{
  "rating": "PG",
  "ratingSource": "USA_PR"
}
```

---

### Parental Ratings

The following parental ratings can be used to better help your viewers find age-appropriate content:

* 12
* 12A
* 14+
* 14A
* 15
* 18
* 18+
* 18A
* A
* AA
* C
* C8
* E
* G
* NC17
* PG
* PG13
* R
* R18
* TV14
* TVG
* TVMA
* TVPG
* TVY
* TVY14
* TVY7
* U
* Uc
* UNRATED

### Rating Sources

These are the accepted values for the `ratingSource` property followed by their meaning:

* BBFC - British Board of Film Classification
* CHVRS - Canadian Home Video Rating System
* CPR - Canadian Parental Rating
* MPAA - Motion Picture Association of America
* UK_CP - UK Content Provider
* USA_PR - USA Parental Rating

---

## credit
Child object of property:

* `movie`
* `series`
* `series` -> `episodes` -> `episode`
* `shortFormVideo`
* `tvSpecial`

This object represents a single person in the credits of a video content.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| name | string | required | name of the person
| role | enum | required | role of the person - must be one of the following values:<br><ul><li>actor</li><li>anchor</li><li>host</li><li>narrator</li><li>voice</li><li>director</li><li>producer</li><li>screenwriter</li></ul>
| birthDate | string | required | birthdate of the person

**Credit Object Example:**

``` json
{
  "name": "Douglas N. Adams",
  "role": "screenwriter",
  "birthDate": "1952-03-11"
}
```

---

## adBreak
Child object of property:

* `content`

This object represents an ad break video content.

| Field | Type | Required | Description |
| ----- | ---- | -------- | ----------- |
| cuePoint | float | required | The cuepoint or offset for when the ad should be inserted.
| duration | integer | required | The duration of the ad.
| name | string | optional | The name of the ad event.

**AdBreak Object Example:**

``` json
{
  "name": "Ad 1",
  "cuePoint": 781.6266699999999,
  "duration": 120
}
```

---


## References

* JSON Schema Draft 4: http://json-schema.org/latest/json-schema-core.html
* ISO 8601: http://www.iso.org/iso/home/standards/iso8601.htm
* JSON Schema Validator: http://www.jsonschemavalidator.net/
* JSON Schema Lint: http://jsonschemalint.com/draft4/
