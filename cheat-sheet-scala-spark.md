# Scala with spark cheat-sheet
Based on the [Big Data Analysis with Scala and Spark](https://courseware.epfl.ch/courses/course-v1:EPFL+scala-spark-big-data+2018-T1/) online course

## RDD
The workhorse of Spark is the RDD (Resilient Distributed Dataset).

There are 2 types of operations for RDDs:
1. Transformations - produces a new RDD from the existing RDD. They are **lazy**, the resulting RDD is not immediately computed 
2. Actions (eager) - Compute a result based on an RDD. They are **eager**, their result is immediately computed

## Common transformations on RDDs
```
val xs = RDD(...)
xs map f        // Apply function f to each element in   the ROD and retrun an  ROD of  the result
xs flatMap f    // Apply a  function to  each element in  the ROD and return an  ROD of  the contents of the iterators returned
xs filter pred  // Apply predicate function to  each element in  the  ROD and return an  ROD of  elements that have passed the predicate condition, pred.
xs.distinct     // Return ROD with duplicates removed
```

## Common actions on RDDs
```
val xs = RDD(...)

// Also present in Scala collections
xs.collect                      // Return all elements from RDD
xs.count                        // Return the number of elements in the  RDD
xs.take(n)                      // Return the first n elements of the  RDD
xs reduce op                    // Combine the elements in  the RDD  together using op function and return result
xs foreach f                    // Apply function f to each element in  the  RDD
xs.aggregate(zv)(seqOp, combOp) // Aggregate the elements of each partition, and then the results for all the partitions, using given combine functions and a neutral "zero value"

// Not in Scala collections
xs.takeSample(withRepl, num)        // Return an array with a random sample of num elements of the dataset, with or without replacement.
xs.takeOrdered(num)(implicit ord)   // Return the  first  n  elements of  the  ROD  using either their natural order or a custom comparator
xs.saveAsTextFile(path)             // Write the  elements of  the  dataset as  a  text  file  in the local filesystem or  HDFS
xs.saveAsSequenceFile(path)         // Write the  elements of  the  dataset as  a  Hadoop  Se­quenceFile in the local filesystem or HDFS
```

## Caching and persistence
xs.cache                    // Cache the RDD in memory, do not recompute. Useful if you need to reuse the dataset

xs.persist(storageLevel)    // Allows the specification of the [storage level](https://spark.apache.org/docs/latest/rdd-programming-guide.html#which-storage-level-to-choose)

## Common transformations on two RDDs
```
val xs = RDD(...)
val ys = RDD(...)

xs union ys         // Return an  RDD  containing elements from both RDDs.
xs intersection ys  // Return an RDD   containing elements only found in both RDDs
xs substract ys     // Return an  RDD  with the contents of  the other RDD removed
xs cartesian ys     // Cartesian product with the  other RDD
```

## Common transformations on RDDs of (key, value) pairs (= PairRDDFunctions)
```
val xs = RDD((k1, v1), (k2, v2), (k3, v3), ...)
xs.groupByKey       // Group the values for each key in the RDD into a single sequence
xs reduceByKey f    // Merge the values for each key using an associative and commutative reduce function
xs mapValues f      // Pass each value in the key-value pair RDD through a map function without changing the keys
```