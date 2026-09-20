name: Generate Pink Snake

on:
  schedule:
    - cron: "0 0 * * *"
  workflow_dispatch:

jobs:
  generate:
    permissions:
      contents: write

    runs-on: ubuntu-latest

    steps:
      - name: Generate pink contribution snake
        uses: Platane/snk/svg-only@v3
        with:
          github_user_name: Modhini-IT

          outputs: |
            dist/github-contribution-grid-snake.svg?color_snake=#ff4f9a&color_dots=#fff5fa,#ffd6e7,#ffadc8,#ff79aa,#ff3b8d
            dist/github-contribution-grid-snake-dark.svg?color_snake=#ff69b4&color_dots=#161b22,#54213a,#96365e,#d94d82,#ff69b4

      - name: Publish snake
        uses: peaceiris/actions-gh-pages@v4
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_branch: gh-pages
          publish_dir: ./dist
