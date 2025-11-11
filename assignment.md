# Assignment

## Brief

Write the Python codes for the following questions.

## Instructions

Paste the answer as Python in the answer code section below each question.

### Question 1

Question: From the `movies` collection, return the documents with the `plot` that starts with `"war"` in acending order of released date, print only title, plot and released fields. Limit the result to 5.

Answer:

```python
# Select database and collection
db = client["sample_mflix"]
collection = db["movies"]

# Build query
query = {"plot": {"$regex": "^war", "$options": "i"}}  # plot starts with "war" (case-insensitive)
projection = {"_id": 0, "title": 1, "plot": 1, "released": 1}

# Execute query
result = (
    collection
    .find(query, projection)
    .sort("released", 1)   # ascending order
    .limit(5)
)

# Print results
for movie in result:
    print(movie)
```

### Question 2

Question: Group by `rated` and count the number of movies in each.

Answer:

```python
# Select database and collection
db = client["sample_mflix"]
collection = db["movies"]

# Aggregation pipeline
pipeline = [
    {"$group": {"_id": "$rated", "count": {"$sum": 1}}},
    {"$sort": {"count": -1}}  # optional, sorts by count descending
]

# Run the aggregation
result = collection.aggregate(pipeline)

# Print results
for doc in result:
    print(doc)
```

### Question 3

Question: Count the number of movies with 3 comments or more.

Answer:

```python
db = client["sample_mflix"]
collection = db["movies"]

count = collection.count_documents({"num_mflix_comments": {"$gte": 3}})
print(count)
```

## Submission

- Submit the URL of the GitHub Repository that contains your work to NTU black board.
- Should you reference the work of your classmate(s) or online resources, give them credit by adding either the name of your classmate or URL.
