# AI-Powered-Fuel-Efficient-Route-Optimization-Project

Project Overview:

This project moves beyond traditional navigation by developing a system to find the most fuel-efficient route between two points, rather than just the shortest or fastest. By creating a custom "fuel cost" metric based on road distance and elevation, this project demonstrates how graph theory and external APIs can be combined to solve complex, real-world logistics problems.

The final output is an interactive map that visually compares the standard shortest route with the calculated eco-friendly route, providing a clear and quantifiable measure of potential fuel savings. This entire analysis was performed on the street network of Vellore, Tamil Nadu, India.

Core Concepts & Methodology
The project was built on a foundation of geospatial data processing and graph theory.

Graph-Based City Model:

The street network of Vellore was downloaded from OpenStreetMap using the OSMnx library and modeled as a mathematical graph, where intersections are nodes and roads are edges.

Elevation Data Integration:

To account for the impact of terrain on fuel consumption, elevation data was crucial. This was fetched by programmatically querying the Open Topo Data public API for every node in the graph.

The project successfully navigated API limitations (like request URI length) by implementing a batching system to retrieve elevation data in smaller chunks.

Proxy Fuel Model:

The key innovation of this project is a proxy model for fuel consumption. Since real fuel data is unavailable, a cost function was engineered and applied to every road (edge) in the graph.

Formula: fuel_cost = (w1 * distance) + (w2 * distance * grade)

This model penalizes uphill travel (grade > 0) significantly more than distance alone, creating a custom weight for route optimization.

Route Optimization with Dijkstra's Algorithm:

Using the NetworkX library, two optimal paths were calculated using Dijkstra's algorithm:

Shortest Route: Used length as the edge weight.

Fuel-Efficient Route: Used our custom fuel_cost as the edge weight.

Visualization:

The final routes were plotted on an interactive Folium map, providing a clear visual comparison between the shortest (blue) and most fuel-efficient (green) paths.

Key Challenges & Solutions
This project involved overcoming several real-world technical challenges, demonstrating robust problem-solving skills:

Outdated Library Functions: The osmnx library has undergone significant updates. The code was systematically debugged and refactored to replace deprecated functions with their modern equivalents, ensuring compatibility and stability.

API Rate Limiting: The initial attempt to fetch elevation data for all nodes in a single API call resulted in a 414 Request-URI Too Large error.

Solution: A batch processing loop was implemented to query the API with smaller, manageable chunks of data, showcasing the ability to work around external service limitations.

API Geographic Coverage: An early attempt used a European-centric elevation dataset, which failed for the Indian location.

Solution: The code was adapted to use a global elevation dataset (mapzen), demonstrating the importance of selecting the correct data sources.

How to Use
Clone the Repository:

git clone https://github.com/your-username/your-repository-name.git

Open in Google Colab:

Upload the .ipynb notebook file to Google Colab.

The notebook is self-contained and will install all necessary dependencies (osmnx, folium).

Run the Cells:

Execute the cells sequentially. The code will download the map data for Vellore, fetch elevation data, apply the fuel model, calculate both routes, and display a final interactive map comparing them.
