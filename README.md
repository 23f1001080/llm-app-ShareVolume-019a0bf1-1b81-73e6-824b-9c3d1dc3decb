# Align Technology Shares Outstanding Viewer

## Project Title and Description
This web application displays the maximum and minimum number of Common Stock Shares Outstanding for a given company, fetched directly from the SEC EDGAR API. Initially, it shows data for Align Technology (ALGN), but it can be updated dynamically to display data for any other publicly traded company by providing its Central Index Key (CIK) in the URL. The data displayed is filtered to include only entries from fiscal years greater than 2020.

## Setup Instructions

To run this application locally, follow these steps:

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```
2.  **Install Node.js and npm:**
    Ensure you have Node.js (which includes npm) installed. You can download it from [nodejs.org](https://nodejs.org/).
3.  **Install dependencies:**
    This project uses `express` for serving static files.
    ```bash
    npm install
    ```
4.  **Generate `data.json` (if not already present):**
    The `data.json` file, which contains the processed information for the default company (Align Technology), is typically pre-generated and committed to the repository. For this project, `data.json` is provided as a static file, reflecting the initial data processing requirements.

5.  **Start the server:**
    ```bash
    npm start
    ```
    The server will start on `http://localhost:3000` (or another available port).

## Usage Guide

1.  **Default View:**
    Open your web browser and navigate to `http://localhost:3000`. The page will load and display the maximum and minimum shares outstanding for **Align Technology, Inc.**, along with the corresponding fiscal years (FY).

2.  **View Data for a Different Company:**
    You can dynamically fetch and display data for any other publicly traded company by appending its 10-digit CIK to the URL as a query parameter.
    For example, to view data for **Apple Inc.** (CIK: 0000320193):
    `http://localhost:3000/?CIK=0000320193`
    (Note: The CIK should be 10 digits, padded with leading zeros if necessary, e.g., `0001018724` for Microsoft).
    The page will update without a full reload to show the new company's data. A loading message will appear during the fetch operation.

## Code Explanation

The project consists of the following key files:

*   **`index.html`**: This is the main front-end file.
    *   It includes a clean, responsive HTML structure with specific `id` attributes for dynamic content updates (`share-entity-name`, `share-max-value`, `share-max-fy`, `share-min-value`, `share-min-fy`).
    *   **Styling (`<style>` tag):** Provides basic CSS for a visually appealing layout.
    *   **JavaScript (`<script>` tag):**
        *   On page load, it checks for a `CIK` query parameter in the URL.
        *   If a `CIK` is provided, it fetches data for that CIK from the SEC EDGAR API using `fetch()`. A public proxy service (AIPipe `allorigins.win`) is used to bypass potential CORS issues when directly accessing the SEC API from the browser.
        *   If no `CIK` is provided, it fetches data for the default company (Align Technology, CIK `0001097149`) from the SEC API.
        *   The fetched data is processed to filter for fiscal years greater than 2020 and to identify the maximum and minimum share values.
        *   The UI is then updated dynamically with the processed information.
*   **`data.json`**: This file contains a pre-processed snapshot of the shares outstanding data for Align Technology (CIK `0001097149`). It serves as an example of the expected data structure and confirms the initial data processing requirements. While `index.html` dynamically fetches data from the SEC API at runtime, this file ensures a static representation of the processed default data is available.
*   **`server.js`**: A minimal Node.js Express server to serve the static files (`index.html`, `data.json`, `uid.txt`, `LICENSE`). It simply makes the local files accessible via HTTP.
*   **`package.json`**: Defines project metadata and lists `express` as a dependency.
*   **`uid.txt`**: A static file containing a unique identifier as specified in the project requirements.
*   **`LICENSE`**: Contains the MIT License details.

## License Information
This project is licensed under the MIT License. See the `LICENSE` file for more details.
