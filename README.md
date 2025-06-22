## API Overview

The MoviesDatabase API (v1) by SAdrian provides access to a rich dataset of over 9 million movies, series, and episodes, along with detailed information on 11 million actors, directors, and crew members. Hosted on RapidAPI, this RESTful API supports keyword-based title search, full title lookups, cast and crew listings, biographies, ratings, trailers, and awards. All requests require X-RapidAPI-Key and X-RapidAPI-Host headers for authentication. Responses are returned in JSON format and support pagination. It's ideal for applications that need comprehensive movie data, with manageable rate limits and reliable performance.

## Version

The current version documented is v1, as indicated in the endpoint URLs and RapidAPI interface.

## Available Endpoints

1. /search/movie

Description: Search for movies by title or keywords.
Typical request:
GET https://moviesdatabase.p.rapidapi.com/titles/search/keyword/{query}

Response: JSON list of titles with IDs, title, year, and type. 2. /title/movie/{id}

Description: Fetch full movie details using its unique ID.
Response: Object with title, synopsis, release date, genres, runtime, trailer, ratings, cast & crew, awards.

3. /title/actor/{id}

Description: Fetch actor or crew member details.
Response: Object including name, birth, bio, filmography, awards.

4. /title/{type}/{id}/credits

Description: Retrieve cast & crew credits for a given title ID.
Response: Array of cast/crew entries (name, role, character).

5. /title/movie/{id}/awards

Description: Get award nominations and wins for a specific title.
Response: List of award ceremonies and related nominations.

## Request and Response Format

Example – Search

GET /titles/search/keyword/inception
X-RapidAPI-Key: YOUR_API_KEY
X-RapidAPI-Host: moviesdatabase.p.rapidapi.com

Response:

{
"results": [
{
"id": "tt1375666",
"title": "Inception",
"year": "2010",
"type": "movie"
},
...
],
"total": 1,
"page": 1,
"limit": 10
}

## Authentication

All requests require two headers:

    X-RapidAPI-Key: your private API key

    X-RapidAPI-Host: moviesdatabase.p.rapidapi.com
    These must be included in every call as per RapidAPI standard.

## Error Handling

Common Error Responses

    401 Unauthorized: Missing/invalid API key

    404 Not Found: Title or actor ID doesn’t exist

    429 Too Many Requests: Rate limit exceeded

    500 Internal Server Error: Temporary server issues

Use try/catch blocks (or language equivalents) to:

    Validate status codes

    Retry on 500 after a short delay

    Stop or delay on 429 (e.g. with exponential backoff or wait until window resets)

## Usage Limits and Best Practices

Rate limits are managed by RapidAPI and depend on your subscription tier (usually e.g. 1000–10,000 calls/day).

Monitor the X-RateLimit-\* headers for your tier usage.

Best practices:

    Cache popular titles and actor results

    Use pagination (page, limit) to minimize data transfer

    Fetch only needed fields (e.g., skip awards if not used)
