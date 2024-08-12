<!--  -->
name: On Release Candidate Branch Creation

on:
  create:
    
jobs:
  open-dev-to-rc-pr:
    name: Open Dev to Release Candidate PR
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      # - name: Check if the creation event is for a branch
      #   if: github.event.ref_type != 'branch'
      #   run: echo "Not a branch creation event, skipping" exit 1
      #   shell: bash

      # - name: Check if the branch name starts with "rc-"
      #   id: check-branch-creation
      #   uses: ./.github/actions/check-branch-creation


      # - name: Open PR
      #   if: steps.check-branch-creation.outputs.result == 'true'
      #   uses: ./.github/actions/open-pr
      #   with:
      #     template: .github/templates/DEV_RC_PR.md
      #     github-token: ${{ secrets.GITHUB_TOKEN }}
      #     base-branch: ${{ github.ref_name }}
      #     branch-with-changes: develop

