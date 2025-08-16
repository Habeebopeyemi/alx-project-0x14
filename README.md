# MoviesDatabase API

## API Overview

The **MoviesDatabase API** provides comprehensive and up-to-date information on over **9 million titles** (movies, series, and episodes) and **11 million actors, crew, and cast members**.  
It delivers detailed data such as:

- Full biographies and filmographies
- Awards and nominations
- YouTube trailer URLs
- Ratings and votes
- Episode and season details
- Revenue and budget figures
- Search functionality for keywords, titles, and alternate names

**Update Frequency**:

- **Recent titles**: Weekly
- **Ratings & episodes (light)**: Daily

---

## Version

**v1.0** (based on provided documentation)

---

## Available Endpoints

### Titles

- **GET `/titles`** — Returns a list of titles based on filters and sorting options.
- **GET `/x/titles-by-ids`** — Returns multiple titles by an array of IMDb IDs.
- **GET `/titles/{id}`** — Returns detailed information for a single title.
- **GET `/titles/{id}/ratings`** — Returns ratings and vote counts for a title.
- **GET `/titles/series/{id}`** — Returns light episode data for a series.
- **GET `/titles/seasons/{id}`** — Returns number of seasons for a series.
- **GET `/titles/series/{id}/{season}`** — Returns light episode data for a specific season.
- **GET `/titles/episode/{id}`** — Returns detailed episode information.
- **GET `/titles/x/upcoming`** — Returns upcoming titles.

### Search

- **GET `/titles/search/keyword/{keyword}`** — Search for titles by keyword.
- **GET `/titles/search/title/{title}`** — Search for titles by name (exact match optional).
- **GET `/titles/search/akas/{aka}`** — Search for titles by alternate names (exact match only).

### Actors

- **GET `/actors`** — Returns a list of actors with optional pagination.
- **GET `/actors/{id}`** — Returns detailed actor information.

### Utils

- **GET `/title/utils/titleType`** — Returns available title types.
- **GET `/title/utils/genres`** — Returns available genres.
- **GET `/title/utils/lists`** — Returns predefined title lists.

---

## Request and Response Format

### Request Example

```http
GET /titles?limit=5&startYear=2020&genre=Action&info=base_info
Host: api.example.com
Authorization: Bearer YOUR_API_KEY
```

### Request Example

```json
{
  "results": [
    {
      "id": "tt1234567",
      "titleText": { "text": "Example Movie" },
      "primaryImage": { "url": "https://image.url" },
      "titleType": { "id": "movie", "text": "Movie" },
      "releaseDate": { "year": 2020, "month": 5, "day": 15 },
      "genres": [{ "text": "Action" }],
      "ratingsSummary": { "aggregateRating": 7.8, "voteCount": 10234 }
    }
  ],
  "page": 1,
  "next": "/titles?page=2",
  "entries": 5
}
```

### Authentication
This API requires authentication via an API key.
Include your key in the request header:
```http
Authorization: Bearer YOUR_API_KEY
```
If the API key is missing or invalid, the request will fail with a `401 Unauthorized` response.

## Error Handling

### Common Errors

- **400 `Bad Request`** — Invalid parameters or malformed request.
- **401 `Unauthorized`** — Missing or invalid API key.
- **404 `Not Found`** — The requested resource could not be found.
- **500 `Internal Server Error`** — A server-side issue occurred.

### Best Practices for Handling Errors

- Always check HTTP status codes before processing the response.
- Log error messages from the response body for debugging.
- Implement retry logic for temporary server errors (5xx status codes).
- Validate all query parameters before sending requests.

### Usage Limits and Best Practices

- **Rate Limits:** — Invalid parameters or malformed request.
- **Pagination:** — Use `limit` and `page` parameters to paginate results instead of fetching large datasets in a single call.
- **Data Caching:** — Cache frequently requested static data (e.g., movie metadata) to reduce unnecessary API calls.
- **Field Selection:** — Use the `info` parameter to request only required fields for performance optimization.
- **Filtering:** - Apply filters such as `genre`, `startYear`, `endYear`, and `titleType` to narrow results and speed up responses.
