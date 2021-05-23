```
printf '{"event_type":"apply_patch","client_payload":{"patch":"%b"}}' \
 "$(base64 -w 0 a.patch)" | \
 curl --request POST \
  --url 'https://api.github.com/repos/dlqs/patch-to-pull-request/dispatches' \
  --header 'authorization: Bearer $GITHUB_TOKEN'\
  --data @-
```
