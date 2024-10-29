import java.util.*;

public class Graph {
    private Map<Integer, List<Integer>> adjList;

    public Graph() {
        adjList = new HashMap<>();
    }

    // Add a vertex to the graph
    public void addVertex(int vertex) {
        adjList.putIfAbsent(vertex, new ArrayList<>());
    }

    // Add an undirected edge between two vertices
    public void addEdge(int source, int destination) {
        adjList.putIfAbsent(source, new ArrayList<>());
        adjList.putIfAbsent(destination, new ArrayList<>());
        adjList.get(source).add(destination);
        adjList.get(destination).add(source); // because the graph is undirected
    }

    // Get the adjacency list for a vertex
    public List<Integer> getAdjVertices(int vertex) {
        return adjList.get(vertex);
    }

    // Depth First Search (DFS)
    public void dfs(int start) {
        Set<Integer> visited = new HashSet<>();
        dfsHelper(start, visited);
    }

    private void dfsHelper(int vertex, Set<Integer> visited) {
        visited.add(vertex);
        System.out.print(vertex + " ");

        for (int neighbor : getAdjVertices(vertex)) {
            if (!visited.contains(neighbor)) {
                dfsHelper(neighbor, visited);
            }
        }
    }

    // Breadth First Search (BFS)
    public void bfs(int start) {
        Set<Integer> visited = new HashSet<>();
        Queue<Integer> queue = new LinkedList<>();

        visited.add(start);
        queue.add(start);

        while (!queue.isEmpty()) {
            int vertex = queue.poll();
            System.out.print(vertex + " ");

            for (int neighbor : getAdjVertices(vertex)) {
                if (!visited.contains(neighbor)) {
                    visited.add(neighbor);
                    queue.add(neighbor);
                }
            }
        }
    }

    @Override
    public String toString() {
        return "Graph{" +
                "adjList=" + adjList +
                '}';
    }
}


import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Graph graph = new Graph();

        // Menu to interact with the graph
        while (true) {
            System.out.println("1. Add Vertex");
            System.out.println("2. Add Edge");
            System.out.println("3. Display Graph");
            System.out.println("4. DFS Traversal");
            System.out.println("5. BFS Traversal");
            System.out.println("6. Exit");
            System.out.print("Enter your choice: ");

            int choice = scanner.nextInt();
            switch (choice) {
                case 1:
                    System.out.print("Enter vertex: ");
                    int vertex = scanner.nextInt();
                    graph.addVertex(vertex);



                    System.out.println("Vertex " + vertex + " added.");
                    break;

                case 2:
                    System.out.print("Enter source vertex: ");
                    int source = scanner.nextInt();
                    System.out.print("Enter destination vertex: ");
                    int destination = scanner.nextInt();
                    graph.addEdge(source, destination);
                    System.out.println("Edge added between " + source + " and " + destination);
                    break;

                case 3:
                    System.out.println("Graph: " + graph);
                    break;

                case 4:
                    System.out.print("Enter starting vertex for DFS: ");
                    int dfsStart = scanner.nextInt();
                    System.out.println("DFS Traversal starting from " + dfsStart + ":");
                    graph.dfs(dfsStart);
                    System.out.println();
                    break;

                case 5:
                    System.out.print("Enter starting vertex for BFS: ");
                    int bfsStart = scanner.nextInt();
                    System.out.println("BFS Traversal starting from " + bfsStart + ":");
                    graph.bfs(bfsStart);
                    System.out.println();
                    break;

                case 6:
                    System.out.println("Exiting...");
                    scanner.close();
                    return;

                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}
