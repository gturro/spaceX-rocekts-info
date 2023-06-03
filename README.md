# SpaceX Rockets Showcase

This is a simple project showcasing the use of Vue.js and API calls to fetch and display data about rockets operated by SpaceX. The project retrieves data from the open-source SpaceX API ([https://api.spacexdata.com/v4/rockets/](https://api.spacexdata.com/v4/rockets/)) and provides a page where users can inspect each rocket with more detailed information.

## Features

- Retrieve data about rockets operated by SpaceX from the SpaceX API
- Display a list of rockets on the main page
- Clicking on a rocket in the list navigates to a detailed page with additional information about the selected rocket

## Prerequisites

Before running this project, make sure you have the following prerequisites installed:

- Node.js: [https://nodejs.org/](https://nodejs.org/)
- Vue CLI: [https://cli.vuejs.org/](https://cli.vuejs.org/)

## Installation

1. Clone this repository:

  ```bash
  git clone <repository-url>
  ```
  
2. Navigate to the project directory:

  ```bash
  cd spacex-rockets-info
  ```
3. Install the project dependencies using npm:

```bash
npm install
```

## Usage
1. Start the development server:
```bash
npm run serve
```
2. Open your browser and visit http://localhost:port to view the application.

### Project Structure

<ul>
  <li><code>src/main.js</code>: The entry point of the application.</li>
  <li><code>src/App.vue</code>: The root component of the application.</li>
  <li><code>src/components/RocketGarden.vue</code>: Component to display the list of rockets.</li>
  <li><code>src/components/RocketViewer.vue</code>: Component to display detailed information about a specific rocket.</li>
  <li><code>src/services/SpaceXService.js</code>: Service to fetch data from the SpaceX API.</li> In proggres...
</ul>

### API Integration
This project utilizes the SpaceX API to fetch data about rockets. The API endpoint used is https://api.spacexdata.com/v4/rockets/. The SpaceXService module in the project handles the API integration and provides methods to fetch the required data.
