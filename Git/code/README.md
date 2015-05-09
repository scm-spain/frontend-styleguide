## Code & Snippets

####List branches & revision date
```
git for-each-ref --sort='-authordate:iso8601' --format=' %(authordate:iso8601)%09%(refname)' refs/heads
```
