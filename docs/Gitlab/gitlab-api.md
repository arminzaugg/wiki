---
Title: Gitlab REST API
---
### Use Gitlab REST API

This page lists a couple useful curl commands to interact with the Gitlab API.

#### pre-requirements
- api endpoint e.g. `export CI_API_V4_URL=https://gitlab.gcp.fenaco.com/api/v4`
- access token e.g. `export PRIVATE_TOKEN=XXXXXXXX`
    
#### helper environment variables
`export MR_PRD_MESSAGE="PRD` Deployment requires CAB approval. Get approval before deploying to PRD."

#### work with gitlab discussions

- create a new discussion thread
```
curl --globoff --location -X POST -H "PRIVATE-TOKEN: $PRIVATE_TOKEN" --data-urlencode "body=test" "$CI_API_V4_URL/projects/60/merge_requests/22/discussions" | jq
```

- get all discussion objects
```
curl -sS -H "PRIVATE-TOKEN: $PRIVATE_TOKEN" "$CI_API_V4_URL/projects/60/merge_requests/22/discussions" | jq
```

- get all discussion objects of type DiscussionNote
```
curl -sS -H "PRIVATE-TOKEN: $PRIVATE_TOKEN" "$CI_API_V4_URL/projects/60/merge_requests/22/discussions" | jq 'map(select(.notes[].type =="DiscussionNote"))'
```
:::info
If no discussions exist API returns `[]`
:::

- get all discussions of type DiscussionNote and with body $MR_PRD_MESSAGE
```
curl -sS -H "PRIVATE-TOKEN: $PRIVATE_TOKEN" "$CI_API_V4_URL/projects/60/merge_requests/22/discussions" | jq --arg MESSAGE "$MR_PRD_MESSAGE" 'map(select(.notes[].type == "DiscussionNote" and .notes[].body == env.MR_PRD_MESSAGE and .notes[].resolved != true))'
```

- get all discussions with body regex match
```
curl -sS -H "PRIVATE-TOKEN: $PRIVATE_TOKEN" "$CI_API_V4_URL/projects/60/merge_requests/45/discussions" | jq 'map(select(.notes[].type ==
 "DiscussionNote" and (.notes[].body | test("^TF PLAN.*" ) )))' | jq '.[].notes[].id'
 ```


- delete notes
`DELETE /projects/:id/merge_requests/:merge_request_iid/discussions/:discussion_id/notes/:note_id
`
example
```
curl --request DELETE -H "PRIVATE-TOKEN: $PRIVATE_TOKEN" "$CI_API_V4_URL/projects/60/merge_requests/45/4642"
```







