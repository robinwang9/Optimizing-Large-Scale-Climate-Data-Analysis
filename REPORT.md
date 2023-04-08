# Lab 4: Dask

- Name: Robin Wang

- NetID: jw5487

## Description of your solution


# Summary

The solution leverages Dask to optimize the computation of the temperature difference. First, I preprocess the data and filter out the unwanted records in the `process_partition` function. This function groups the data by the relevant columns and computes the mean of the values for 'TMAX' and 'TMIN'. This approach helps in reducing the amount of data being processed and stored in memory. Next, I process the files in chunks, convert the results to a Dask DataFrame, and merge the TMAX and TMIN DataFrames.

To further optimize the computation, I concatenate the list of Dask DataFrames, repartition them, and perform a groupby operation on the concatenated Dask DataFrame. The final result is computed and saved as a Parquet file.

# Performance

- Tiny dataset: CPU times: user 438 ms, sys: 108 ms, total: 546 ms, Wall time: 1.93 s
- Small dataset: CPU times: user 7.4 s, sys: 1.11 s, total: 8.51 s, Wall time: 17.5 s
- Large dataset: CPU times: user 15min 10s, sys: 1min 39s, total: 16min 50s, Wall time: 29min 44s

# Optimization strategies

The primary optimization strategy was to preprocess the data in the `process_partition` function to reduce the amount of data being processed and stored in memory. I also processed the files in chunks, which allowed for better parallelization and memory management. Then, I concatenated the list of Dask DataFrames and repartitioned them before performing the final groupby operation, ensuring efficient memory usage and parallel processing.

# Alternative implementations

I tried an alternative implementation that performed operations on the Dask DataFrames without computing the grouped data beforehand. This approach led to less efficient processing and increased memory usage that caused kernel and gateway timeout errors. As a result, I changed my approach and computed the grouped data before performing further operations, reducing memory usage and potentially improving performance.

# Unexpected behavior

I encountered issues related to converting the Dask Series to a DataFrame and saving the final result in Parquet format. I fixed these issues by explicitly converting the Dask Series to a Dask DataFrame and adjusting the code to save the final result as a Parquet file.

Additionally, during the computation, I faced a Gateway Timeout error. Upon inspecting the error log, I discovered that the issue was caused by the IOPub data rate limit. I resolved the issue by modifying the Jupyter Notebook configuration file to increase the data rate limit. After making the necessary changes, I no longer encountered the timeout error.


