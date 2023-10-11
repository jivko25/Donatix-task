# GREET API TASK Documentation

## Table of Contents
1. [Description](#description)
2. [Deployment](#deployment)
3. [Running the Application](#running-the-application)
4. [Functionality](#functionality)

## 1. Description
The "GREET API TASK" application is a Single-Page Application (SPA) designed to consume an external API and present its data in card format. The application is implemented using Vue.js and meets the following requirements:

- Consumes the API endpoint: [https://greet.bg/wp-json/wc/store/products?page=1](https://greet.bg/wp-json/wc/store/products?page=1)
- Presents the API response as cards, with each card containing:
  - An image
  - Name
  - Description
  - Category
  - An "Add To Cart" button
- The "Add To Cart" button leads to the URL [https://greet.bg/?add-to-cart=5589](https://greet.bg/?add-to-cart=5589).
- Implements pagination using infinite scrolling.
- Provides a dropdown for filtering results by category. Categories are dynamically populated based on the loaded data.
- Includes a dropdown for ordering items by name and price.

## 2. Deployment
The application is deployed and accessible online at the following URL: [GREET API TASK](https://donatix-task.vercel.app/).

## 3. Running the Application
To run the application locally, follow these steps:

### Prerequisites
- Node.js and npm (Node Package Manager) installed on your system.

### Installation
1. Clone the Git repository to your local machine.
   ```bash
   git clone <repository_url>
2. Change your working directory to the project folder.

  ```bash
  cd <project_folder>
  ```

3. Install the project's dependencies using npm.

  ```bash
  npm install
  ```

4. Once the installation is complete, you can start the development server to run the application.

  ```bash
  npm run serve
  ```

The application will be running at a local development server, usually at http://localhost:8080/. You can open this URL in your web browser to view the application.

5. Functionality
The "GREET API TASK" application allows users to browse a list of products retrieved from the specified API endpoint. Users can interact with the application as follows:

View a list of product cards, each displaying product details.
Click the "Add To Cart" button on any card to be directed to the cart for the corresponding product.
Perform infinite scrolling to load more products as they scroll down the page.
Use the category dropdown to filter products by category.
Use the order dropdown to sort products by name and price in both ascending and descending order.
Note: The application is a Vue.js SPA and utilizes dynamic data from the provided API endpoint.
