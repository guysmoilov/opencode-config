---
description: Fetch and summarize unresolved PR comments for the current branch
agent: explore
---
Fetch the PR comments for the current repository and the current branch using the GitHub CLI (`gh`). 

To correctly identify unresolved issues, you should:
1. Identify the current branch and its associated PR number.
2. Use the GitHub GraphQL API to fetch `reviewThreads`, filtering for only unresolved ones. You can use a command like this:
   ```bash
    gh api graphql -F owner='OWNER' -F name='REPO' -F number=PR_NUMBER -f query='
    query($owner: String!, $name: String!, $number: Int!) {
      repository(owner: $owner, name: $name) {
        pullRequest(number: $number) {
          reviewThreads(first: 100) {
            nodes {
              isResolved
              comments(last: 10) {
                nodes {
                  id
                  body
                  author { login }
                  reactionGroups {
                    content
                    viewerHasReacted
                  }
                }
              }
            }
          }
        }
      }
    }' --jq '.data.repository.pullRequest.reviewThreads.nodes[] | select(.isResolved == false)'
    ```
3. For unresolved threads, extract the discussion history, focusing on the latest concerns and any reactions from the current user (e.g., 👍). Use `viewerHasReacted` to filter for your own reactions.

Provide a concise summary categorized by topic (e.g., Security, Architecture, Naming). For each point, mention which user(s) raised the concern and note if you (the current viewer) have reacted (e.g., with a Thumbs Up 👍) to indicate agreement or acknowledgement. Exclude any comments that have already been marked as resolved.

