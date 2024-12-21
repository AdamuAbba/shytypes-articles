- [X] implement reply to comment
	- [x] move comment handler to submit button
- [] implement like a comment
	- No endpoint for like a comment
- [] show UI to load insight comment reply
	- load comment reply
- Refactor comment component (In progress)

> [!bug]
> - getInsightsByCommentId name and profilePictureUrl are null

```json
{
"data": {
"getInsightCommentByID": {
"id": "da3ea334-a96c-4298-82a2-de8550a21945",
"accountID": "5abe5310-376e-4f73-a6d7-5c4aa14a2c8d",
"insightID": "4fc74b05-f4ee-4a6a-9d11-078dc3c60a20",
"commentID": "",
"content": "Test",
"name": null,
"profilePictureURL": null,
"comments": [
"1c948f05-79f6-4020-aee0-f2108c46e2d5"
],
"createdAt": "2024-12-15T15:26:18.103659Z",
"updatedAt": "2024-12-15T15:26:18.103659Z"
}
}
}
```