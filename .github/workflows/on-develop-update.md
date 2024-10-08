name: On Develop Update

on:
  push:
    branches:
      - develop

jobs:
  open-rc-pr:
    name: Open RC PR
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Get current version and build number
        id: get-current-version-info
        uses: ./.github/actions/get-current-version-info
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - name: Open PR
        uses: ./.github/actions/open-pr
        with:
          template: .github/templates/DEV_RC_PR.md
          github-token: ${{ secrets.GITHUB_TOKEN }}
          base-branch: rc-v${{ steps.get-current-version-info.outputs.version }}
          branch-with-changes: develop
