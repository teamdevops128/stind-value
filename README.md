#!/bin/bash

ORG_NAME="niti"
SEARCH_STRING="@abhi.com"
GITHUB_TOKEN="your_personal_access_token"

API_URL="https://api.github.com/search/code?q=${SEARCH_STRING}+org:${ORG_NAME}"

response=$(curl -s -H "Accept: application/vnd.github.v3+json" -H "Authorization: token $GITHUB_TOKEN" "$API_URL")

CSV_FILE="string.csv"
echo "File Name,File Path,Full Name" > "$CSV_FILE"
echo "$response" | jq -r '.items[] | "\(.name),\(.path),\(.repository.full_name)"' >> "$CSV_FILE"

echo "CSV file saved as $CSV_FILE"
