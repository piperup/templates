---
mode: "agent"
description: "Update Existing GitHub Issue to Match Template"
tools:
  - search
  - github/github-mcp-server/search_issues
  - github/github-mcp-server/issue_read
  - github/github-mcp-server/issue_write
  - github/github-mcp-server/add_issue_comment
---

# Format GitHub Issue

Reformat and review an existing GitHub issue ${input:issue_number:Issue number on GitHub} to match the correct template in `.github/ISSUE_TEMPLATE/`.

## Steps

1. **Verify Issue**

   - Use #github/github-mcp-server/search_issues to confirm the issue exists.
   - If it does **not** exist, stop immediately (do not create a new issue).
   - If inaccessible, return:
     ```
     Error: Could not access issue ${input:issue_number:Issue number on GitHub}. No changes made.
     ```

2. **Read Existing Issue**

   - Retrieve the issue’s title, body, and metadata using #github/github-mcp-server/issue_read tool.

3. **Find the Appropriate Template**

   - Use #search tool to list all files under `.github/ISSUE_TEMPLATE/`.
   - For each template:
     - Read its frontmatter (`name`, `about`, etc.).
     - Compare issue title/body keywords against template keywords.
     - Choose the template with the **highest contextual match**.
   - If no strong match is found:
     - Use defaults:
       - `bug_report.md` for crashes, errors, or reproducible problems.
       - `feature_request.md` for suggestions or new ideas.
     - If still unclear, leave the issue unchanged and return:
       ```
       No suitable template match found. Issue left as-is.
       ```

4. **Reformat the Issue**

   - Rebuild the issue body using **only** the fields from the chosen template.
   - Fill in known fields from the existing issue content.
   - For missing fields, use `N/A`.
   - Maintain the **exact structure** and section order of the template.
   - Do **not** remove or add extra sections.

5. **Update the Title**

   - Keep the original title if it’s already descriptive.
   - If vague, improve it slightly (≤15 words) while keeping the same meaning and tone.

6. **Preserve Voice and Tone**

   - Retain the author's original language, writing style, and sentiment.
   - You **may** improve clarity, grammar, or organization, but **must not** remove any factual information provided by the author.
   - Preserve exact wording where possible—only modify when necessary for readability or template compliance.
   - If clarification is needed, add minimal context without changing the author's voice or intent.

7. **Optional: Preview Step (if enabled)**

   - Before updating, return the reformatted issue for review.
   - Example:
     ```
     Preview generated for review — confirm before writing.
     ```

8. **Write Updated Issue**

   - Use #github/github-mcp-server/issue_write tool to replace the issue’s body and/or title with the reformatted content.

9. **Add a Review and Suggest Improvements**

   Perform a content review to enhance the issue’s usefulness by suggesting possible directions.

   When to Use:

   - The issue is vague or lacks actionable details.
   - The author’s intent is clear but missing references, methods, or next steps.

   Guidelines:

   - Offer non-intrusive, constructive, and informative additions.
   - Suggest, but do not impose, possible improvements such as:
     - Potential solutions or approach outlines.
     - Relevant methods, functions, or API endpoints.
     - Helpful examples.
     - Common troubleshooting steps or best practices.

10. **Add Comment with Review**

    - Use #github/github-mcp-server/add_issue_comment tool to append a comment with the review and suggestions.

## Output

Return the updated issue in the following format:

```markdown
<!-- Using template: .github/ISSUE_TEMPLATE/[template-name].md -->

**Title:** [Updated or original title]

[Filled-in template fields]
```

If no update was performed, return the appropriate error or status message.

## Rules

- Only modify existing issues — never create new ones.
- Follow the selected template’s structure exactly.
- Keep titles clear, concise, and meaningful.
- Preserve the author’s tone and intent.
- If unsure about formatting or template choice, err on the side of minimal change.
- Templates should be read from the repository’s `.github/ISSUE_TEMPLATE/` directory via the repository content API (not local filesystem).
