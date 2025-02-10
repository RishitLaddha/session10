# Polygon Class 

## **Overview**  

The `Polygon` class models **regular polygons**, where all sides and angles are equal. It takes two parameters:  

1. **Number of vertices (or edges)** – Determines the shape of the polygon.  
2. **Circumradius** – The radius of the **circumscribed circle**, which encloses the polygon.  

This class provides methods to compute various geometric properties, including **side length, area, perimeter, interior angle, and apothem**. Additionally, it allows for **comparisons** between polygons based on their attributes.


## **Attributes and Properties**  

The `Polygon` class exposes several **properties**, making it easy to retrieve relevant geometric values without explicitly calling methods.

### **Fundamental Properties**  

- **count_vertices**: Returns the number of vertices (or edges) of the polygon.  
- **count_edges**: Identical to `count_vertices`, since a polygon always has equal numbers of edges and vertices.  
- **circumradius**: Returns the circumradius, which defines the size of the polygon in relation to its enclosing circle.  

### **Geometric Properties**  

- **interior_angle**: Computes the interior angle of the polygon. As the number of vertices increases, the angle approaches **180 degrees** (like a circle).  
- **side_length**: Calculates the length of each edge using **trigonometric functions** based on the circumradius.  
- **apothem**: The perpendicular distance from the center of the polygon to the midpoint of any edge. This is useful for calculating the area.  
- **area**: Computes the total area of the polygon using the apothem and side length.  
- **perimeter**: Returns the sum of all edges, calculated as the product of `count_edges` and `side_length`.  


## **Comparison Methods**  

This class supports direct comparisons between polygon instances based on their structural properties.

- **Equality (`==`)**: Two polygons are **equal** if they have the same number of edges and the same circumradius.  
- **Greater than (`>`)**: A polygon is **greater than** another if it has more edges, meaning it is closer to a circular shape.  

These comparison methods enable direct sorting and filtering of polygon objects.



## **Usage**  

The `Polygon` class can be instantiated by specifying the number of edges (or vertices) and the circumradius.  

For example, creating a **hexagon** (6-sided polygon) with a circumradius of **2 units**:  

```python
polygon = Polygon(6, 2)
```

Once a `Polygon` object is created, its properties can be accessed easily:  

- `polygon.count_vertices` → Returns `6`  
- `polygon.interior_angle` → Returns the interior angle of a hexagon  
- `polygon.area` → Computes the total area of the hexagon  
- `polygon.perimeter` → Computes the total perimeter  

### **Comparing Polygons**  

Polygons can also be **compared** based on their structure:  

```python
polygon1 = Polygon(3, 10)  # Triangle
polygon2 = Polygon(6, 10)  # Hexagon

print(polygon1 < polygon2)  # True, since hexagon has more edges
print(polygon1 == polygon2)  # False, since they have different edge counts
```




# Polygons & PolygonIterator 

## **Overview**  

1. **Polygons (Iterable):** A collection of polygons starting from a **triangle** and going up to a polygon with a specified number of sides.  
2. **PolygonIterator (Iterator):** A helper that moves through the sequence of polygons, returning one polygon at a time until all have been accessed.  

By implementing these, the module allows polygons to be iterated over efficiently without manual indexing or tracking.


## **Polygons as an Iterable**  

The `Polygons` class acts as an iterable, representing a collection of polygons of increasing sides. Instead of storing all polygons at once, it generates them dynamically when requested. This approach avoids unnecessary memory usage and ensures that polygons are only created when needed.  

Since an iterable does not directly manage iteration, the `Polygons` class provides two key features:  

- **Access to specific polygons** using indexing.  
- **The ability to return an iterator** that handles step-by-step traversal.  

When the `Polygons` class is used in a loop or any iteration context, it does not iterate by itself but **returns an instance of `PolygonIterator`**, which takes over the iteration process.



## **PolygonIterator as the Iterator**  

The `PolygonIterator` class is responsible for stepping through the sequence of polygons one by one. It starts at the first polygon and progresses forward each time it is called. Once all polygons have been accessed, it automatically stops iteration.  

Since the iterator remembers its position in the sequence, it ensures that each polygon is accessed in order without requiring manual index tracking.  

This design allows the `Polygons` class to function naturally in loops, where each iteration retrieves the next polygon **without extra logic from the user**.



## **How Iteration Works in This Module**  

1. **Creating an Iterable (`Polygons`)**  
   - The iterable represents a sequence of polygons, starting from a **triangle** and increasing in sides.  
   - It does not store all polygons but generates them when needed.  

2. **Returning an Iterator (`PolygonIterator`)**  
   - When iteration begins, the iterable **provides an instance of `PolygonIterator`**, which knows how to retrieve polygons in order.  
   - This allows the `Polygons` class to work naturally in loops without requiring explicit indexing.  

3. **Iterating Through the Sequence**  
   - The iterator starts at the first polygon and moves forward, returning each polygon as requested.  
   - Once the sequence is exhausted, it stops automatically, preventing unnecessary checks or errors.  

4. **Finding the Most Efficient Polygon**  
   - The iterable also provides a way to determine which polygon in the sequence has the highest ratio of **area to perimeter**.  
   - This is done by comparing all polygons in the sequence and selecting the most efficient one.  
