# search_hithub_users

This is a description of the project.

## Getting Started

To use the project, follow these steps:

1. Install the project dependencies: `npm install`
2. Run the project: `npm run serve`

## Features

1. **Display a welcome message**: Upon initial visit to the website, users are greeted with a welcome message.
2. **Show loading**: After entering input in the search field, a loading screen is displayed to indicate that the search is in progress.
3. **Display GitHub users**: Once the loading is complete, the website displays the GitHub usernames and profile avatars of the search results. Users can click on the avatars to navigate to the respective personal websites.
4. **Show errors**: If an error occurs during the search process, an error message is displayed on the screen to inform users about the issue.
5. **API endpoint**: The functionality utilizes the API endpoint https://api.github.com/search/users to fetch the GitHub user data.

## Packages
```
"dependencies": {
    "axios": "^1.4.0",
    "core-js": "^3.8.3",
    "element-plus": "^2.3.4",
    "mitt": "^3.0.0",
    "vue": "^3.2.13"
  }
```
