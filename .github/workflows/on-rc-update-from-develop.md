name: Trigger on PR merge on RC branch from Develop

on:
  pull_request:
    branches:
      - "rc-v*"
    types:
      - closed
  
jobs:
  open-pr-to-main:
    name: Open PR to main
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      - name: Check PR Info
        id: check-merged-pr
        uses: ./.github/actions/check-merged-pr
        with:
          expected-base-branch-prefix: rc-v
          expected-head-branch-prefix: develop
          
      - name: Open PR to main
        id: open-pr-to-main
        if: steps.check-merged-pr.outputs.result == 'true'
        uses: ./.github/actions/open-pr
        with:
          template: .github/templates/RC_MAIN_PR.md
          github-token: ${{ secrets.ADMIN_GITHUB_TOKEN }}
          base-branch: main
          branch-with-changes: ${{github.event.pull_request.base.ref}}
