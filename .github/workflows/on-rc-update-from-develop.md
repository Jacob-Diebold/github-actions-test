<!-- TODO: Edit the trigger to only run on PRs from develop to rc branch -->
name: On Release Candidate Update

on:
  push:
    branches:
      - "rc-v*"
  
jobs:
  submit-staging-build:
    name: Submit Staging Build
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v4
      
      - name: Submit Staging Build
        uses: ./.github/actions/submit-build
        with:
          expo-token: ${{ secrets.EXPO_TOKEN }}
          release-channel: staging
  # TODO: Increment build number & create a pr to main