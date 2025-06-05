Created: 2025-06-05 17:30
-- -
# Key Concepts:
#### Works:
By default, the search endpoint returns _works_ instead of _editions_. A **work** is a collection of editions; for example there is only one work for The Wonderful Wizard of Oz, but there are 1029 editions, over many languages.
# Requests:
### Paginated Work Search
```
https://openlibrary.org/search.json?q=the+eye+of+the+world&language=eng&limit=1&page=1
```
#### Parameters
- `q=the+eye+of+the+world`: User text search
- `limit=1&page=1`: Pagination params
- `language=eng`: Filter by english language
#### Result
```json
       {
            "author_key": [
                "OL233594A"
            ],
            "author_name": [
                "Robert Jordan"
            ],
            "cover_edition_key": "OL8890304M",
            "cover_i": 980232,
            "ebook_access": "borrowable",
            "edition_count": 69,
            "first_publish_year": 1990,
            "has_fulltext": true,
            "ia": [
                "larouedutempslin0000robe",
                "loeildumonde0000jord",
                "dasradderzeit2da0000jord",
                "shijiezhiyan0001qiao",
                "eyeofworldjord00jord",
                "eyeofworldthewhe00robe",
                "eyeofworld0000jord",
                "eyeofworld00robe",
                "eyeofworld00jord",
                "eyeworld00jord"
            ],
            "ia_collection_s": "americana;cnusd-ol;delawarecountydistrictlibrary;denverpubliclibrary-ol;goffstownlibrary-ol;inlibrary;internetarchivebooks;ithacacollege-ol;library_of_atlantis;miltonpubliclibrary-ol;openlibrary-d-ol;popularchinesebooks;printdisabled;riceuniversity-ol;spokanepubliclibrary-ol;tulsacc-ol;unb-ol;universityofarizona-ol;universityofcoloradoboulder-ol;worthingtonlibraries-ol",
            "key": "/works/OL7924103W",
            "language": [
                "spa",
                "eng",
                "ger",
                "fre",
                "per",
                "por",
                "chi"
            ],
            "lending_edition_s": "OL28342659M",
            "lending_identifier_s": "larouedutempslin0000robe",
            "public_scan_b": false,
            "title": "The Eye of the World (The Wheel of Time Book 1)"
        }
```
### Specific Work
```
https://openlibrary.org/works/OL7924103W.json
```
#### Parameters
- `OL7924103W`: `key` field on the previous search response.
#### Response
```json
{
  "title": "The Eye of the World (The Wheel of Time Book 1)",
  "key": "/works/OL7924103W",
  "authors": [
    {
      "author": {
        "key": "/authors/OL233594A"
      },
      "type": {
        "key": "/type/author_role"
      }
    }
  ],
  "type": {
    "key": "/type/work"
  },
  "covers": [980232, 2182401, 182341, 603075, 908780, 8784284, 8785931, 603208, 2056268, 9588941, 6878658, 10398333, 11404766, 13731417, 12144286, 14082812, 8456088, 8623997, 8631611, 8784016, 10674102, 12283128, 12294052, 12353462, 14286611, 8565631, 8634730, 10290889, 13839835, 14286610, 14286609],
  "description": "The Wheel of Time turns and Ages come and go, leaving memories that become legend. Legend fades to myth, and even myth is long forgotten when the Age that gave it birth returns again. In the Third Age, an Age of Prophecy, the World and Time themselves hang in the balance. What was, what will be, and what is, may yet fall under the Shadow.",
  "subjects": [
    "series:The Wheel of Time",
    "Fantasy fiction",
    "Rand al'Thor (Fictitious character)",
    "Fiction",
    "Reader recommended, 2001-02",
    "Fantasy .",
    "American Fantasy",
    "al'Thor Rand (Fictitious character)",
    "Good and evil",
    "Monsters",
    "Rand al'thor (fictitious character), fiction",
    "Fiction, fantasy, epic",
    "Science fiction",
    "Children's fiction",
    "Fiction, fantasy, general",
    "Comics & graphic novels, fantasy",
    "Comic books, strips",
    "nyt:hardcover-graphic-books=2013-02-17",
    "New York Times bestseller",
    "Fantasy",
    "Children's stories",
    "American literature"
  ],
  "identifiers": {
    "bookbrainz": [
      "a4a33937-33a0-4486-97d8-23e6550a8402"
    ],
    "musicbrainz": [
      "3e9ce6a2-3f7f-4418-b7d5-2ea49b72573d"
    ],
    "wikidata": [
      "Q477994"
    ]
  },
  "latest_revision": 6,
  "revision": 6,
  "created": {
    "type": "/type/datetime",
    "value": "2009-12-10T22:13:35.559002"
  },
  "last_modified": {
    "type": "/type/datetime",
    "value": "2025-01-29T13:17:58.881496"
  }
}
```
### Get Editions of a Specific Work
```
https://openlibrary.org/works/OL7924103W/editions.json
```
#### Parameters
- `OL7924103W`: Same `key` as the previous search
#### Result (Partial)
```json
    {
      "works": [
        {
          "key": "/works/OL7924103W"
        }
      ],
      "title": "Zenica Sveta",
      "publishers": [
        "Laguna"
      ],
      "publish_date": "2022",
      "key": "/books/OL59253777M",
      "type": {
        "key": "/type/edition"
      },
      "identifiers": {

      },
      "covers": [15091959],
      "publish_places": [
        "Serbia"
      ],
      "physical_format": "Hardcover",
      "number_of_pages": 576,
      "isbn_13": [
        "9788652147144"
      ],
      "series": [
        "Točak vremena"
      ],
      "latest_revision": 5,
      "revision": 5,
      "created": {
        "type": "/type/datetime",
        "value": "2025-06-05T06:07:47.578423"
      },
      "last_modified": {
        "type": "/type/datetime",
        "value": "2025-06-05T07:22:22.493825"
      }
    },
```
### Specific Edition
```
https://openlibrary.org/books/OL59253777M.json
```
#### Parameters
- `OL59253777M`: `key` field in previous search response
#### Result
Same result as previous search partial result
### Paginated Author Search
```
https://openlibrary.org/search/authors.json?q=sanderson
```
#### Result
```json
    {
      "alternate_names": [
        "BRANDON SANDERSON",
        "Sanderson  Brandon",
        "B. Sanderson",
        "Sanderson, Brandon",
        "Sanderson, B.",
        "2023 Tor Author to be Announced"
      ],
      "birth_date": "19 December 1975",
      "key": "OL1394865A",
      "name": "Brandon Sanderson",
      "top_subjects": [
        "Fiction, fantasy, general",
        "Fiction",
        "Fiction, fantasy, epic",
        "Fantasy",
        "Fantasy fiction",
        "New York Times bestseller",
        "Children's fiction",
        "Magic",
        "Fiction, science fiction, general",
        "Science fiction"
      ],
      "top_work": "The Final Empire",
      "type": "author",
      "work_count": 175,
      "ratings_average": 4.3639603,
      "ratings_sortable": 4.323879,
      "ratings_count": 1404,
      "ratings_count_1": 4,
      "ratings_count_2": 34,
      "ratings_count_3": 155,
      "ratings_count_4": 465,
      "ratings_count_5": 746,
      "want_to_read_count": 4102,
      "already_read_count": 2224,
      "currently_reading_count": 242,
      "readinglog_count": 6568,
      "_version_": 1.8272832642193818e+18
    },
```
### Specific Author
```
https://openlibrary.org/authors/OL1394865A.json
```
- `OL1394865A` : `key` field on the previous search response.
#### Result
```json
{
  "birth_date": "19 December 1975",
  "source_records": [
    "amazon:1511359935",
    "amazon:0593567854",
    "amazon:9123988622",
    "ia:steelheart0000sand_g0e1",
    "amazon:6053753068",
    "amazon:8418037423",
    "bwb:9781938570322",
    "amazon:1616964022",
    "bwb:9781399602150",
    "amazon:8374800801",
    "amazon:0593433874",
    "bwb:9780575097391",
    "promise:bwb_daily_pallets_2022-03-17",
    "promise:bwb_daily_pallets_2023-01-27:KS-155-150",
    "amazon:8375069418",
    "bwb:9781803364674",
    "bwb:9781466877726",
    "promise:bwb_daily_pallets_2023-10-11:W8-ADQ-239",
    "bwb:9781399614931",
    "bwb:9781399622325",
    "bwb:9781250899675",
    "marc:harvard_bibliographic_metadata/ab.bib.13.20150123.full.mrc:544131434:810"
  ],
  "links": [
    {
      "title": "Official Author's Website",
      "url": "http://www.brandonsanderson.com/",
      "type": {
        "key": "/type/link"
      }
    },
    {
      "title": "Amazon Author Page",
      "url": "http://www.amazon.com/Brandon-Sanderson/e/B001IGFHW6",
      "type": {
        "key": "/type/link"
      }
    },
    {
      "title": "Goodreads Author Page",
      "url": "http://www.goodreads.com/author/show/38550.Brandon_Sanderson",
      "type": {
        "key": "/type/link"
      }
    },
    {
      "title": "The Coppermind Wiki - 17th Shard, the Official Brandon Sanderson Fansite",
      "url": "https://coppermind.net/wiki/",
      "type": {
        "key": "/type/link"
      }
    },
    {
      "title": "17th Shard, the Official Brandon Sanderson Fansite",
      "url": "https://www.17thshard.com/",
      "type": {
        "key": "/type/link"
      }
    },
    {
      "title": "Official FAQ Website",
      "url": "https://faq.brandonsanderson.com/",
      "type": {
        "key": "/type/link"
      }
    }
  ],
  "type": {
    "key": "/type/author"
  },
  "alternate_names": [
    "BRANDON SANDERSON",
    "Sanderson  Brandon",
    "B. Sanderson",
    "Sanderson, Brandon",
    "Sanderson, B.",
    "2023 Tor Author to be Announced"
  ],
  "personal_name": "Brandon Sanderson",
  "photos": [14851192, 7252549],
  "remote_ids": {
    "wikidata": "Q457608",
    "viaf": "50418535",
    "isni": "0000000114724577",
    "bookbrainz": "272a2e3c-159a-4469-a62a-b8fabb0380e4",
    "musicbrainz": "b7b9f742-8de0-44fd-afd3-fa536701d27e",
    "goodreads": "38550",
    "librarything": "sandersonbrandon",
    "lc_naf": "n2004036176",
    "imdb": "nm7124506",
    "gnd": "133523829",
    "youtube": "UC3g-w83Cb5pEAu5UmRrge-A",
    "amazon": "B001IGFHW6",
    "storygraph": "2ee3fed7-9bff-4a19-868c-d194ca72ce26"
  },
  "bio": "Brandon Sanderson (born December 19, 1975) is an American author known for his intricate and imaginative works in the genres of fantasy and science fiction. Born in Lincoln, Nebraska, Sanderson developed a passion for writing at a young age. He attended Brigham Young University, where he studied English and later earned a master's degree in creative writing.\r\n\r\nSanderson is best known for creating the Cosmere, a vast fictional universe that encompasses many of his fantasy novels, where they share subtle connections and a common mythology, including the *Mistborn* series and *The Stormlight Archive*. The *Mistborn* trilogy, starting with the novel [*Mistborn: The Final Empire*][3], is a thrilling fantasy heist story set in a dystopian world ruled by a tyrannical lord. *The Stormlight Archive*, starting with the novel [*The Way of Kings*][8], is an epic fantasy series that combines political intrigue, war, and extensive world-building.\r\n\r\nIn addition to his work within the Cosmere, Sanderson completed [Robert Jordan's][4] epic fantasy series \"The Wheel of Time\" after Jordan's passing. He has also authored several young adult series, such as *The Reckoners* and the *Skyward* series.\r\n\r\nSanderson's analytical approach to world-building includes his \"Sanderson's Laws of Magic,\" which distinguish between \"hard\" and \"soft\" magic systems in fantasy literature. His ability to create immersive worlds and compelling characters has earned him a dedicated fan base and numerous accolades, including the Hugo Award in 2013 for his novella [*The Emperor's Soul*][5], the Romantic Times Reviewers' Choice Award for his novels [*Elantris*][6] in 2005, and [The Hero of Ages][7] in 2008, as well as David Gemmell Legend Awards in 2011 for [*The Way of Kings*][8] and in 2015 for [*Words of Radiance*][9]. In 2022, Sanderson's Kickstarter campaign for four secret novels became the most successful in history, raising over $41 million.\r\n\r\nAs of 2022, he is a co-creator and former host of the *Writing Excuses* podcast, an educational podcast for writers by writers that was started in 2008.\r\n\r\n(Sources: [1][1],[2][2])\r\n\r\n[1]: https://www.brandonsanderson.com/pages/hello-my-names-brandon\r\n[2]: https://en.wikipedia.org/wiki/Brandon_Sanderson\r\n[3]: https://openlibrary.org/works/OL5738148W\r\n[4]: https://openlibrary.org/authors/OL233594A\r\n[5]: https://openlibrary.org/works/OL19960448W\r\n[6]: https://openlibrary.org/works/OL5738147W\r\n[7]: https://openlibrary.org/works/OL5738154W\r\n[8]: https://openlibrary.org/works/OL15358691W\r\n[9]: https://openlibrary.org/works/OL16813053W",
  "key": "/authors/OL1394865A",
  "name": "Brandon Sanderson",
  "latest_revision": 37,
  "revision": 37,
  "created": {
    "type": "/type/datetime",
    "value": "2008-04-01T03:28:50.625462"
  },
  "last_modified": {
    "type": "/type/datetime",
    "value": "2025-03-19T13:10:09.177353"
  }
}
```
### Specific Author Photos
```
https://covers.openlibrary.org/a/id/14851192-M.jpg
```
#### Parameters
- `14851192-M`: IDs stored in the `photos` field on the previous search response
# Happy Lifecycle:
## Specific Work Edition search
1. User Searches Paginated Works, gets desired `Work Key`
2. User uses `Work Key` to Search Specific Work, gets Work Data and option to see `Work Editions`.
3. User uses `Work Editions List` to get desired `Edition Key`
## Author search
1. User Searches Paginated Authors, gets desired `Author Key`
2. User uses `Author Key` to Search Specific Author and Specific Author Photos