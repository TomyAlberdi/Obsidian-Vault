Created: 2025-06-02 19:17
-- -
# Google Books API
##### Volume
A volume represents the data that google books hosts about a book or magazine. Its the primary resource in the Books API. All other resources in this API either contain or annotate a volume.
**Volume ID**:
Unique strings given to each volume that Google Books knows about. An example of a volume ID is `_LettPDhwR0C`. You can use the API to get the volume ID by making a request that returns a Volume resource; you can find the volume ID in its `id` field.
### Queries
Placeholder volume search query:
```
https://www.googleapis.com/books/v1/volumes?q=search+terms
```
This request has a single required parameter:
- ` q ` - Search for volumes that contain this text string. There are special keywords you can specify in the search terms :
	- `intitle`
	- `inauthor`
	- `inpublisher`
	- `subject` (Results where the text following is listed in the category list of the volume)
Example search query for Daniel Keyes' "Flowers for Algernon":
```
GET https://www.googleapis.com/books/v1/volumes?q=flowers+inauthor:keyes&key=yourAPIKey
```
> Note: Performing a search does not require authentication, so you do not have to provide the `Authorization` HTTP header with the `GET` request. However, if the call is made with authentication, each Volume will include user-specific information, such as purchased status.

If the request succeeds, the server responds with a `200 OK` HTTP status code and the volume results:
```json
200 OK

{
 "kind": "books#volumes",
 "items": [
  {
   "kind": "books#volume",
   "id": "_ojXNuzgHRcC",
   "etag": "OTD2tB19qn4",
   "selfLink": "https://www.googleapis.com/books/v1/volumes/_ojXNuzgHRcC",
   "volumeInfo": {
    "title": "Flowers",
    "authors": [
     "Vijaya Khisty Bodach"
    ],
   ...
  },
  {
   "kind": "books#volume",
   "id": "RJxWIQOvoZUC",
   "etag": "NsxMT6kCCVs",
   "selfLink": "https://www.googleapis.com/books/v1/volumes/RJxWIQOvoZUC",
   "volumeInfo": {
    "title": "Flowers",
    "authors": [
     "Gail Saunders-Smith"
    ],
    ...
  },
  {
   "kind": "books#volume",
   "id": "zaRoX10_UsMC",
   "etag": "pm1sLMgKfMA",
   "selfLink": "https://www.googleapis.com/books/v1/volumes/zaRoX10_UsMC",
   "volumeInfo": {
    "title": "Flowers",
    "authors": [
     "Paul McEvoy"
    ],
    ...
  },
  "totalItems": 3
}
```
#### Optional Standard Query Parameters:
- `maxResults`: The maximum number of results to return. The default is 10, and the maximum allowable value is 40.
- `orderBy`: By default, a search request returns results ordered by most relevant first.
  You can change the ordering by setting the `orderBy` parameter to be one of these values:
	- `orderBy=relevance` - Returns search results in order of the most relevant to least (this is the default).
	- `orderBy=newest` - Returns search results in order of the newest published date to the oldest.
- `startIndex`: For any request for all items in a collection, you can paginate results by specifying `startIndex` and `maxResults` in the parameters for the request. The index of the first item is 0.
#### Retrieving a specific volume
You can retrieve information for a specific volume by sending an HTTP `GET` request to the Volume resource URI:
```
https://www.googleapis.com/books/v1/volumes/volumeId
```
Replace the `volumeId` path parameter with the ID of the volume to retrieve. See the [Google Books IDs](https://developers.google.com/books/docs/v1/using#ids) section for more information on volume IDs.
Here is an example of a `GET` request that gets a single volume:
```
GET https://www.googleapis.com/books/v1/volumes/zyTCAlFPjgYC?key=yourAPIKey
```
If the request succeeds, the server responds with the `200 OK` HTTP status code and the Volume resource requested:
```json
200 OK

{
 "kind": "books#volume",
 "id": "zyTCAlFPjgYC",
 "etag": "f0zKg75Mx/I",
 "selfLink": "https://www.googleapis.com/books/v1/volumes/zyTCAlFPjgYC",
 "volumeInfo": {
  "title": "The Google story",
  "authors": [
   "David A. Vise",
   "Mark Malseed"
  ],
  "publisher": "Random House Digital, Inc.",
  "publishedDate": "2005-11-15",
  "description": "\"Here is the story behind one of the most remarkable Internet
  successes of our time. Based on scrupulous research and extraordinary access
  to Google, ...",
  "industryIdentifiers": [
   {
    "type": "ISBN_10",
    "identifier": "055380457X"
   },
   {
    "type": "ISBN_13",
    "identifier": "9780553804577"
   }
  ],
  "pageCount": 207,
  "dimensions": {
   "height": "24.00 cm",
   "width": "16.03 cm",
   "thickness": "2.74 cm"
  },
  "printType": "BOOK",
  "mainCategory": "Business & Economics / Entrepreneurship",
  "categories": [
   "Browsers (Computer programs)",
   ...
  ],
  "averageRating": 3.5,
  "ratingsCount": 136,
  "contentVersion": "1.1.0.0.preview.2",
  "imageLinks": {
   "smallThumbnail": "https://books.google.com/books?id=zyTCAlFPjgYC&printsec=frontcover&img=1&zoom=5&edge=curl&source=gbs_api",
   "thumbnail": "https://books.google.com/books?id=zyTCAlFPjgYC&printsec=frontcover&img=1&zoom=1&edge=curl&source=gbs_api",
   "small": "https://books.google.com/books?id=zyTCAlFPjgYC&printsec=frontcover&img=1&zoom=2&edge=curl&source=gbs_api",
   "medium": "https://books.google.com/books?id=zyTCAlFPjgYC&printsec=frontcover&img=1&zoom=3&edge=curl&source=gbs_api",
   "large": "https://books.google.com/books?id=zyTCAlFPjgYC&printsec=frontcover&img=1&zoom=4&edge=curl&source=gbs_api",
   "extraLarge": "https://books.google.com/books?id=zyTCAlFPjgYC&printsec=frontcover&img=1&zoom=6&edge=curl&source=gbs_api"
  },
  "language": "en",
  "infoLink": "https://books.google.com/books?id=zyTCAlFPjgYC&ie=ISO-8859-1&source=gbs_api",
  "canonicalVolumeLink": "https://books.google.com/books/about/The_Google_story.html?id=zyTCAlFPjgYC"
 },
 "saleInfo": {
  "country": "US",
  "saleability": "FOR_SALE",
  "isEbook": true,
  "listPrice": {
   "amount": 11.99,
   "currencyCode": "USD"
  },
  "retailPrice": {
   "amount": 11.99,
   "currencyCode": "USD"
  },
  "buyLink": "https://books.google.com/books?id=zyTCAlFPjgYC&ie=ISO-8859-1&buy=&source=gbs_api"
 },
 "accessInfo": {
  "country": "US",
  "viewability": "PARTIAL",
  "embeddable": true,
  "publicDomain": false,
  "textToSpeechPermission": "ALLOWED_FOR_ACCESSIBILITY",
  "epub": {
   "isAvailable": true,
   "acsTokenLink": "https://books.google.com/books/download/The_Google_story-sample-epub.acsm?id=zyTCAlFPjgYC&format=epub&output=acs4_fulfillment_token&dl_type=sample&source=gbs_api"
  },
  "pdf": {
   "isAvailable": false
  },
  "accessViewStatus": "SAMPLE"
 }
}
```
### Performance Tips
#### Partial Resources
A way to improve the performance of your API calls is by sending and receiving only the portion of the data that you're interested in. This lets your application avoid transferring, parsing, and storing unneeded fields, so it can use resources including network, CPU, and memory more efficiently.
##### Partial Response
By default, the server sends back the full representation of a resource after processing requests. For better performance, you can ask the server to send only the fields you really need and get a _partial response_ instead.
To request a partial response, use the `fields` request parameter to specify the fields you want returned. You can use this parameter with any request that returns response data.
Example:
The following example shows the use of the `fields` parameter with a generic (fictional) "Demo" API.
**Simple request:** This HTTP `GET` request omits the `fields` parameter and returns the full resource.
```
https://www.googleapis.com/demo/v1
```
**Full resource response:** The full resource data includes the following fields, along with many others that have been omitted for brevity.
```json
{
  "kind": "demo",
  ...
  "items": [
  {
    "title": "First title",
    "comment": "First comment.",
    "characteristics": {
      "length": "short",
      "accuracy": "high",
      "followers": ["Jo", "Will"],
    },
    "status": "active",
    ...
  },
  {
    "title": "Second title",
    "comment": "Second comment.",
    "characteristics": {
      "length": "long",
      "accuracy": "medium"
      "followers": [ ],
    },
    "status": "pending",
    ...
  },
  ...
  ]
}
```
**Request for a partial response:** The following request for this same resource uses the `fields` parameter to significantly reduce the amount of data returned.
```
https://www.googleapis.com/demo/v1?fields=kind,items(title,characteristics/length)
```
**Partial response:** In response to the request above, the server sends back a response that contains only the kind information along with a pared-down items array that includes only HTML title and length characteristic information in each item.
```json
{
  "kind": "demo",
  "items": [{
    "title": "First title",
    "characteristics": {
      "length": "short"
    }
  }, {
    "title": "Second title",
    "characteristics": {
      "length": "long"
    }
  },
  ...
  ]
}
```
Note that the response is a JSON object that includes only the selected fields and their enclosing parent objects.
Details on how to format the `fields` parameter is covered next, followed by more details about what exactly gets returned in the response.
The format of the `fields` request parameter value is loosely based on XPath syntax. The supported syntax is summarized below, and additional examples are provided in the following section.
- Use a comma-separated list to select multiple fields.
- Use `a/b` to select a field `b` that is nested within field `a`; use `a/b/c` to select a field `c` nested within `b`.  
    **Exception:** For API responses that use "data" wrappers, where the response is nested within a `data` object that looks like `data: { ... }`, do not include "`data`" in the `fields` specification. Including the data object with a fields specification like `data/a/b` causes an error. Instead, just use a `fields` specification like `a/b`.
- Use a sub-selector to request a set of specific sub-fields of arrays or objects by placing expressions in parentheses "`( )`".
    For example: `fields=items(id,author/email)` returns only the item ID and author's email for each element in the items array. You can also specify a single sub-field, where `fields=items(id)` is equivalent to `fields=items/id`.
- Use wildcards in field selections, if needed.
    For example: `fields=items/pagemap/*` selects all objects in a pagemap.