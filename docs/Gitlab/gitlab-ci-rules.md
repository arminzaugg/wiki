---
Title: Gitlab CI Rules
---

### Gitlab CI Rules

Before we can start using rules, we must understand variables. They come from a lot of different places, like:
- CI/CD Configuration
- Default Gitlab variables
- Genrated from previous jobs
- Project/Group configuration

[Predefiend variables](https://docs.gitlab.com/ee/ci/variables/predefined_variables.html) are not meant to be overwritten, but can be used in Rules. Some of them are very common:
- `CI_API_V4_URL` - API base url of Gitlab instance
- `CI_COMMIT_BRANCH` - Branch name

:::danger
Do not wrap Gitlab variables in {}-braces. Just use e.g. $CI_JOB_TOKEN. Only use this in scripts.
:::

### Pipeline Triggers

Pipelines can be triggered by any of the following events:
- new commit
- new branch
- new tag
- manual
- api call
- scheduled

### Rules Components
What can one use to create rules?


| Clause  | Operators | Results       | When Options |
|---------|-----------|---------------|--------------|
| if      | ==        | when          | always       |
| changes | !=        | allow_failure | never        |
| exists  | =~        | start_in      | on_success   |
| "none"  | !~        |               | on_failure   |
|         | &&        |               | manual       |
|         | \|\|      |               | Delayed      |
|         |           |               | "none"       |

#### Clauses
- if
- changes
- exists
- (... or none)

#### Operators
- `==`
- `!=`
- `=~`
- `!=`
- `!~`
- `&&`
- `||`

#### Results
- when
- allow_failure
- start_in

#### "when options"
- always
- never
- on_success
- on_failure
- manual
- Delayed
- (... or none)
    

### Examples

```
rules:
    - if: ${CI_COMMIT_BRANCH} ~= /^release\/.*$/
      when: always
```














