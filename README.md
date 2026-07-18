# Task-4
import math

def euclidean_distance(p1, p2):
    """Calculate Euclidean distance between two points."""
    return math.sqrt(sum((a - b) ** 2 for a, b in zip(p1, p2)))


def k_means(points, k, initial_centroids, max_iterations):
    # Initialize centroids
    centroids = [list(c) for c in initial_centroids]

    for _ in range(max_iterations):

        # Step 1: Create empty clusters
        clusters = [[] for _ in range(k)]

        # Step 2: Assign each point to the nearest centroid
        for point in points:
            distances = [euclidean_distance(point, centroid) for centroid in centroids]
            nearest = distances.index(min(distances))
            clusters[nearest].append(point)

        # Step 3: Compute new centroids
        new_centroids = []

        for i in range(k):
            if clusters[i]:
                dimension = len(points[0])

                centroid = []
                for d in range(dimension):
                    mean = sum(point[d] for point in clusters[i]) / len(clusters[i])
                    centroid.append(mean)

                new_centroids.append(centroid)
            else:
                # Keep the old centroid if cluster is empty
                new_centroids.append(centroids[i])

        # Step 4: Check for convergence
        if new_centroids == centroids:
            break

        centroids = new_centroids

    # Round to 4 decimal places
    result = []
    for centroid in centroids:
        result.append(tuple(round(x, 4) for x in centroid))

    return result


# Example
points = [
    (1, 2),
    (1, 4),
    (1, 0),
    (10, 2),
    (10, 4),
    (10, 0)
]

k = 2

initial_centroids = [
    (1, 1),
    (10, 1)
]

max_iterations = 10

print(k_means(points, k, initial_centroids, max_iterations))
