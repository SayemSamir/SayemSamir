name: Latest blog post workflow

on:
  schedule:
    # Runs every day at 00:00 UTC — change if you want a different frequency
    - cron: '0 0 * * *'
  workflow_dispatch:
  push:
    branches:
      - main

jobs:
  update-readme-with-blog:
    name: Update this repo's README with latest blog posts
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Pull in dev.to posts
        uses: gautamkrishnar/blog-post-workflow@v1
        with:
          comment_tag_name: 'devto'
          feed_list: 'https://dev.to/feed/REPLACE_DEVTO_USERNAME'
          max_post_count: 5

      - name: Pull in Medium posts
        uses: gautamkrishnar/blog-post-workflow@v1
        with:
          comment_tag_name: 'medium'
          feed_list: 'https://medium.com/feed/@REPLACE_MEDIUM_USERNAME'
          max_post_count: 5

      - name: Pull in personal blog posts
        uses: gautamkrishnar/blog-post-workflow@v1
        with:
          comment_tag_name: 'personal'
          feed_list: 'REPLACE_PERSONAL_BLOG_RSS_URL'
          max_post_count: 5
