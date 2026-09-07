# 01 - Basics

## What I learned

### General
- OpenAPI spec is written in YAML (or JSON) — it's a description, not code (no logic, no loops)
- YAML uses indentation (spaces, not tabs) to show nesting — same idea as Python
- Comments in YAML use `#`

### Core structure
- Every spec needs three top-level things:
  - `openapi` — which version of the OpenAPI standard this file follows (e.g. `3.0.0`)
  - `info` — metadata: `title` (API name) and `version` (MY api's version — unrelated
    to the `openapi:` version number, even though they look similar)
  - `paths` — where all actual endpoints are defined

### Paths and methods
- A path is written as a key, e.g. `/books/{id}`
- `{id}` inside a path is a placeholder — a real value replaces it when the endpoint
  is actually called (e.g. `/books/42`)
- Under a path, HTTP methods (`get`, `post`, `put`, `delete`) are declared as separate
  keys. One path can support multiple methods, each described independently.

### Parameters
- Anything in the path like `{id}` must be formally declared under `parameters`
  (otherwise OpenAPI doesn't know it exists as a real input)
- Each parameter needs:
  - `name` — must match the placeholder in the path exactly (`{id}` → `name: id`)
  - `in` — where the value comes from: `path` | `query` | `header`
  - `required` — whether it must be provided (path params are always `true`)
  - `schema.type` — what type of value it is (`string`, `integer`, etc.)

### Responses
- `responses` describes every possible outcome of a request, keyed by HTTP status
  code (e.g. `'200'`) — status codes are written in quotes since YAML would
  otherwise read them as numbers
- Just a `description` alone is only a human-readable note — it doesn't describe
  actual data
- To describe the real response data:
  - `content` → the wrapper for describing the body
  - `application/json` → the media type / format of the body
  - `schema` → the actual shape of the JSON
    - `type: object` → it's a JSON object (`{ }`)
    - `properties` → lists each field and its `type` (string, integer, boolean, etc.)

## Files in this folder
- `stage1-skeleton.yaml` — minimal valid spec: `openapi`, `info`, empty `paths`
- `stage2-one-endpoint.yaml` — added one GET endpoint with just a summary + description
- `stage3-parameters.yaml` — formally declared the `{id}` path parameter
- `stage4-response-body.yaml` — added a real JSON response body via `content` → `schema`

## Things that confused me
- (add your own — e.g. "took a second to get that `name: id` in parameters has to
  match `{id}` in the path exactly, or it silently doesn't work")

## Next up
- Reusable schemas via `components/schemas` and `$ref` — avoid repeating the same
  `properties` block (like the book object) every time it's needed