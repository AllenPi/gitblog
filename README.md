## Gitblog
My personal blog using issues and GitHub Actions (随意转载，无需署名)

modified by [yihong0618](https://raw.githubusercontent.com/yihong0618/gitblog)

[RSS Feed](https://raw.githubusercontent.com/AllenPi/gitblog/master/feed.xml)


# gitblog




<!--START_SECTION:my_github-->

name: GitHub README STATS

on:
  workflow_dispatch:
  schedule:
    - cron: "0 0 * * *"
  push:
    branches:
      - main

env:
  GITHUB_NAME: yihong0618
  GITHUB_EMAIL: zouzou0208@gmail.com
  STARED_NUMBER: 10

jobs:
  build:
    name: Build
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - name: My GitHub Status
        uses: AllenPi/github-readme-stats@main
        with:
          # if you also want to send TELE
          TELEGRAM_TOKEN: ${{ secrets.TELE_TOKEN }}
          TELEGRAM_CHAT_ID: ${{ secrets.TELE_CHAT_ID }}
          STARED_NUMBER: ${{ env.STARED_NUMBER }}

      - name: Push README
        uses: github-actions-x/commit@v2.6
        with:
          github-token: ${{ secrets.G_T }}
          # In this example, you can also use the ${{ secrets.GITHUB_TOKEN }} variable 
          # Permissions for the GITHUB_TOKEN : https://docs.github.com/en/free-pro-team@latest/actions/reference/authentication-in-a-workflow#permissions-for-the-github_token
        
          # If you need more precise Token permission control , you can create a personal access token and set it as a secret in your repository .
          commit-message: "Refresh README (GITHUB STATUS)"
          files: README.md
          rebase: "true"
          name: ${{ env.GITHUB_NAME }}
          email: ${{ env.GITHUB_EMAIL }}

<!--END_SECTION:my_github-->