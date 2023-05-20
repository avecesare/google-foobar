from itertools import permutations
#Bellman-Ford alg: computes shortest paths from a single source vertex to all of the other vertices in a weighted digraph.
def findDistance(graph, src):
    n = len(graph)
    distance = [float('inf')] * n # Initialize distances to infinity for all vertices
    distance[src] = 0 # Distance from source vertex to itself is 0

    for i in range(n):
        for u in range(n):
            for v in range(n):
                weight = graph[u][v]
                if distance[u] + weight < distance[v]:
                    distance[v] = distance[u] + weight # Update the distance if a shorter path is found
    return distance

def bellmanFord(graph):
    distances = []
    for vertex in range(len(graph)):
        distances.append(findDistance(graph, vertex)) # Compute shortest distances from each vertex using Bellman-Ford
    return distances

def negativeCycle(graph):
    distance = graph[0]
    n = len(graph)
    for u in range(n):
        for v in range(n):
            weight = graph[u][v]
            if distance[u] + weight < distance[v]:
                return True # If negative cycle is found, return True
    return False # If no negative cycle, return Fals
            

def getPathTime(bunnies, graph):
    time = 0
    time += graph[0][bunnies[0]]
    time += graph[bunnies[-1]][len(graph)-1]
    for i in range(1, len(bunnies)):
        u = bunnies[i-1]
        v = bunnies[i]
        time += graph[u][v] # Add the time to reach each consecutive pair of bunnies

    return time
def solution(times, times_limit):
    n_bunnies = len(times) - 2
    bunnies = [x for x in range(1, n_bunnies+1)] # List of all bunny indices (excluding start and exit)

    distances = bellmanFord(times) # Compute shortest distances using Bellman-Ford
    if negativeCycle(distances): # Check for negative cycle
        return range(n_bunnies) # If negative cycle exists, all bunnies can be saved
    for i in range(n_bunnies, 0, -1):
        for perm in permutations(bunnies, i): # Generate all permutations of bunny indices
            time = getPathTime(perm, distances)
            if time <= times_limit:
                return[x-1 for x in sorted(perm)] # If a valid permutation is found, return sorted list
    return[] # If no valid permutation is found, return an empty list
    
