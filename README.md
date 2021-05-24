# Patch-to-Pull-Request

Create a GitHub pull request by simply POST-ing a `patch` file! This is a zero-depedency commit workflow, without needing `git clone` etc.

1. Create a Personal Access Token [here](https://github.com/settings/tokens/new) with `workflow` and `repo` scopes. 
   - Unfortunately, tokens cannot be scoped to individual repositories, so creating a dedicated "bot" user who has full admin access to the relevant repository might be an option.
3. Create a `patch` file with `diff`: `diff -u <old file> <new file> > a.patch`
4. POST your patch with `curl`:
```
printf '{"event_type":"apply_patch","client_payload":{"patch":"%b"}}' \
 "$(base64 -w 0 a.patch)" | \
 curl --request POST \
  --url 'https://api.github.com/repos/<username>/<repository>/dispatches' \
  --header 'authorization: Bearer <personal access token>\
  --data @-
```
